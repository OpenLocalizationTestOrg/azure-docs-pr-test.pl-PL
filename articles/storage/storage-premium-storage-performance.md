---
title: "Usługa Azure Premium Storage: Projektować pod kątem wydajności | Dokumentacja firmy Microsoft"
description: "Projektowanie aplikacji wysokiej wydajności przy użyciu usługi Azure Premium Storage. Magazyn w warstwie Premium oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach/O wykonujących obciążeń uruchomionych na maszynach wirtualnych platformy Azure."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: 75845eb4707e8e5606153a5e1a7c10b4113ee121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Magazynu Azure Premium: Projekt o wysokiej wydajności
## <a name="overview"></a>Omówienie
Ten artykuł zawiera wskazówki dotyczące tworzenia aplikacji wysokiej wydajności przy użyciu usługi Azure Premium Storage. Możesz użyć hello instrukcje zawarte w tym dokumencie, w połączeniu z wydajności najlepszych praktyk stosowanych tootechnologies używanych przez aplikację. tooillustrate hello wytycznych, użyliśmy program SQL Server uruchomiony na magazyn w warstwie Premium, na przykład w tym dokumencie.

Gdy wydajność scenariusze hello warstwy magazynu w tym artykule można rozwiązać, konieczne będzie warstwy aplikacji hello toooptimize. Na przykład w przypadku hostowania farmy programu SharePoint w usłudze Azure Premium Storage, można użyć hello przykłady programu SQL Server z tego artykułu toooptimize hello bazy danych serwera. Ponadto Zoptymalizuj farmy programu SharePoint hello serwera sieci Web i aplikacji serwera tooget hello większości.

Ten artykuł pomoże odpowiedzi po często zadawane pytania dotyczące optymalizacji wydajności aplikacji w usłudze Azure Premium Storage

* Jak toomeasure wydajność aplikacji?  
* Dlaczego są nie widać oczekiwanego wysokiej wydajności?  
* Jakie czynniki wpływają wydajność aplikacji na magazyn w warstwie Premium?  
* Jak te czynniki wpływają wydajność aplikacji na magazyn w warstwie Premium  
* Jak można zoptymalizować IOPS, przepustowości i opóźnień?  

Firma Microsoft umieściła wytyczne specjalnie z myślą o magazyn w warstwie Premium ponieważ obciążeń uruchomionych na magazyn w warstwie Premium są wysokiej wydajności poufnych. Firma Microsoft umieściła przykłady, gdzie jest to odpowiednie. Można także zastosować niektóre z tych tooapplications wytyczne działające na maszynach wirtualnych IaaS z dyskami magazynu w warstwie standardowa.

Przed rozpoczęciem, jeśli są tooPremium nowego magazynu, najpierw przeczytać hello [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](storage-premium-storage.md) i [skalowalności magazynu Azure i cele wydajności](storage-scalability-targets.md)artykułów.

## <a name="application-performance-indicators"></a>Wskaźniki wydajności aplikacji
Możemy oceny, czy aplikacja działa również lub nie używa wydajności, takich jak wskaźniki, tempa aplikacji przetwarza żądanie użytkownika, jak dużo danych przetwarza aplikację na żądanie, ile żądań przetwarza aplikacji w określonej okres czasu, jak długo użytkownik ma toowait tooget odpowiedzi po przesłaniu żądania. Witaj terminów tych wskaźników wydajności są IOPS, przepustowości lub przepustowości i opóźnień.

W tej sekcji omówimy hello wspólnych wskaźników wydajności w kontekście hello magazyn w warstwie Premium. W hello następujących sekcji, zbieranie wymagania dotyczące aplikacji, przedstawiono sposób toomeasure tych wskaźników wydajności dla aplikacji. W dalszej optymalizacji wydajności aplikacji poznasz hello czynniki wpływające na te wskaźniki i zalecenia toooptimize wydajności je.

## <a name="iops"></a>Operacje wejścia/wyjścia
IOPS to liczba żądań, że aplikacja wysyła toohello dysków w magazynie w ciągu sekundy. Operacji wejścia/wyjścia można odczytać lub zapisać, sekwencyjnych lub losowych. Aplikacje OLTP, takie jak witryny sieci Web platformy handlowej online konieczne tooprocess wiele równoczesnych użytkownik zażąda natychmiast. żądania użytkowników Hello są insert i aktualizowanie transakcji bazy danych, która aplikacja hello musi przetworzyć w odpowiednim. W związku z tym aplikacje OLTP wymagają bardzo wysokiej IOPS. Takie aplikacje będą obsługiwać miliony małych i losowe żądań We/Wy. Jeśli masz takiej aplikacji, należy zaprojektować toooptimize infrastruktury aplikacji hello dla IOPS. W hello później sekcji, *optymalizacji wydajności aplikacji*, omówiono szczegółowo wszystkie czynniki hello, że należy wziąć pod uwagę tooget wysoka liczba IOPS.

Po dołączeniu premium magazynu dysku tooyour wysokiej skali maszyny Wirtualnej, Azure przepisy dla Ciebie gwarantowane liczbę IOPS zgodnie z harmonogramem hello specyfikację dysku. Na przykład dysk P50 inicjuje 7500 IOPS. Każdy dużą skalę rozmiaru maszyny Wirtualnej ma również określonego limitu IOPS może kontynuować działanie. Na przykład standardowe GS5 maszyna wirtualna ma 80 000 IOPS ograniczenia.

## <a name="throughput"></a>Przepływność
Przepływność lub przepustowości jest hello ilość danych, że aplikacja wysyła toohello dysków w magazynie w określonych odstępach czasu. Jeśli aplikacja wykonuje operacje wejścia/wyjścia o dużych rozmiarach jednostki we/wy, wymaga wysokiej przepływności. Aplikacje magazynu danych zwykle tooissue skanowania intensywne operacje dostęp dużej części danych w czasie i często wykonywać operacje zbiorcze. Innymi słowy takich aplikacji wymaga wyższej przepustowości. Jeśli masz takiej aplikacji, należy zaprojektować jego toooptimize infrastruktury przepustowości. W następnej sekcji hello omówiono czynników hello szczegółów tooachieve musisz dostosować to.

Po dołączeniu premium magazynu dysku tooa wysokiej skali maszyny Wirtualnej, Azure przepisy przepływności zgodnie z tym specyfikację dysku. Na przykład dysk P50 inicjuje 250 MB na dysku drugi przepływności. Każdy dużą skalę rozmiaru maszyny Wirtualnej ma również jako określonych limit przepustowości, co może kontynuować działanie. Na przykład standardowe GS5 maszyna wirtualna ma maksymalną przepustowość 2000 MB na sekundę. 

Brak relacji między przepływności i IOPS, jak pokazano w formule hello poniżej.

![](media/storage-premium-storage-performance/image1.png)

Dlatego jest ważne toodetermine hello optymalnej przepływności i IOPS wartości wymagane przez aplikację. Podczas uzyskiwania toooptimize jedną hello innych pobiera dotyczy także. W dalszej części artykułu *optymalizacji wydajności aplikacji*, omówimy w bardziej szczegółowe informacje o optymalizacji IOPS i przepustowość.

## <a name="latency"></a>Opóźnienie
Opóźnienie jest hello czas tooreceive aplikacji pojedyncze żądanie, przesyła toohello magazynu dysków i wysyłać hello odpowiedzi toohello klienta. Jest to miara krytyczne wydajności aplikacji w tooIOPS dodanie i przepustowość. Witaj opóźnienia dysku magazynu premium jest czas hello przyjmuje tooretrieve hello informacji dla żądania i komunikować się jej kopii tooyour aplikacji. Magazyn w warstwie Premium zapewnia stale małe opóźnienia. Jeśli włączysz buforowania na dyski premium magazynu na hoście tylko do odczytu, możesz uzyskać dużo mniejsze opóźnienia odczytu. Omówimy buforowania dysku bardziej szczegółowo w dalszej części artykułu na *optymalizacji wydajności aplikacji*.

Gdy zoptymalizowany tooget Twojej aplikacji wyżej IOPS i przepływności, będzie miało wpływ na powitania opóźnienia aplikacji. Po dostrajania wydajności aplikacji hello, zawsze ocenia hello opóźnienia tooavoid aplikacji hello duże opóźnienie nieoczekiwane zachowanie.

## <a name="gather-application-performance-requirements"></a>Gromadzenie wymagań dotyczących wydajności aplikacji
jest Hello pierwszy krok w projektowaniu wysoka wydajność aplikacji uruchomionych na usłudze Azure Premium Storage, wymagania dotyczące wydajności hello toounderstand aplikacji. Po zebraniu wymagania dotyczące wydajności, aby zoptymalizować aplikacji tooachieve hello najbardziej optymalną wydajność.

W poprzedniej sekcji hello możemy wyjaśniono hello typowych wskaźników wydajności, IOPS, przepustowości i opóźnień. Należy określić, które z tych wskaźników wydajności są krytyczne tooyour aplikacji toodeliver hello potrzeby użytkowników. Na przykład wysokiej IOPS sprawach większość aplikacji tooOLTP przetwarzania miliony transakcje na sekundę. Wysokiej przepływności jest krytyczne dla magazynu danych aplikacji przetwarzania dużych ilości danych na sekundę. Bardzo małe opóźnienia jest kluczowa dla aplikacji w czasie rzeczywistym, takich jak wideo na żywo przesyłania strumieniowego witryn sieci Web.

Następnie zmierzyć hello wymagania maksymalną wydajność aplikacji przez cały cykl jej życia. Użyj listy kontrolnej próbki hello poniżej jako rozpoczęcia. Wymagania dotyczące maksymalnej wydajności hello rekordów podczas normalnego, okresów obciążenia szczytowego i poza godzinami szczytu. Przez ustalenie wymagań dotyczących wszystkich poziomów obciążeń, będą mogli toodetermine hello ogólne wymagania dotyczące działania aplikacji. Na przykład hello zwykłe obciążenie pracą witryną internetową handlu elektronicznego będzie transakcje hello służy ona większość dni w roku. obciążenia szczytowego Hello hello witryny sieci Web będzie transakcje hello służy ona podczas zdarzenia specjalne sprzedaży lub świąt. obciążenia szczytowego Hello jest zwykle doświadczenie w ograniczonym okresie, ale może wymagać Twojej aplikacji tooscale dwa lub więcej razy swoich normalnych operacji. Dowiedz się hello 50. percentyl, percentyl 90 i wymagania percentyl 99. Dzięki temu odfiltrowywania żadnych wartości odstających w hello wymagania dotyczące wydajności i można skupić się wysiłków na optymalizacji dla prawej wartości hello.

**Lista kontrolna wymagań dotyczących wydajności aplikacji**

| **Wymagania dotyczące wydajności** | **50. percentyl** | **Percentyl 90** | **Percentyl 99** |
| --- | --- | --- | --- |
| Maksymalnie z Transakcje na sekundę | | | |
| Operacje odczytu % | | | |
| Operacje zapisu % | | | |
| % Losowe operacje | | | |
| % Kolejnych operacji. | | | |
| Rozmiar żądania We/Wy | | | |
| Średnia przepustowość | | | |
| Maksymalnie z Przepływność | | | |
| Min. Opóźnienie | | | |
| Średni czas oczekiwania | | | |
| Maksymalnie z Procesor CPU | | | |
| Średnie wykorzystanie Procesora | | | |
| Maksymalnie z Memory (Pamięć) | | | |
| Średnia pamięci | | | |
| Głębokość kolejki | | | |

> [!NOTE]
> Należy rozważyć skalowania tych numerów oparte na oczekiwany przyszłego rozwoju aplikacji. Jest tooplan dobrym rozwiązaniem, wzrost wcześniejsze, ponieważ może on być trudniejsze toochange hello infrastruktury dla poprawy wydajności później.
>
>

Jeśli korzystasz z istniejącej aplikacji i chcesz tooPremium toomove magazynu, należy najpierw utworzyć listę kontrolną hello powyżej hello istniejącej aplikacji. Następnie, tworzenie prototypów aplikacji na magazyn w warstwie Premium i projekt aplikacji hello według wskazówek opisanych w *optymalizacji wydajności aplikacji* w dalszej części tego dokumentu. Witaj następnej sekcji opisano narzędzia hello można użyć miary wydajności hello toogather.

Utworzenie listy kontrolnej podobne tooyour istniejących aplikacji do hello prototypu. Za pomocą narzędzi Benchmarking można symulować hello obciążeń i pomiaru wydajności na powitania prototypu aplikacji. Zobacz sekcję hello na [Benchmarking](#benchmarking) toolearn więcej. Wykonując, dzięki czemu można określić, czy magazyn w warstwie Premium mogą odpowiadać lub przekroczenia wymagań dotyczących wydajności aplikacji. Następnie można wdrożyć hello tych samych wskazówek dla aplikacji produkcyjnej.

### <a name="counters-toomeasure-application-performance-requirements"></a>Wymagania dotyczące wydajności aplikacji toomeasure liczników
Witaj najlepsze sposób toomeasure wymagania dotyczące wydajności aplikacji, toouse monitorowania wydajności narzędzi dostarczanych przez system operacyjny hello powitania serwera. Można użyć Monitora wydajności dla systemu Windows i iostat dla systemu Linux. Te narzędzia przechwytywania liczniki odpowiedniej miar tooeach wyjaśniono w hello powyżej sekcji. Gdy aplikacja jest uruchomiona, jej normalny, obciążeń szczycie i poza godzinami szczytu konieczne jest przechwycenie hello wartości tych liczników.

Liczniki Monitora wydajności Hello są dostępne dla procesora, pamięci, a każdy dysk logiczny i dysku fizycznego serwera. Użycie dysków w warstwie premium magazynu z maszyny Wirtualnej, są hello dysku fizycznego liczniki dla każdego dysku magazynu premium i są dysku logicznego liczniki dla każdego woluminu tworzone na dyskach magazynu premium hello. Konieczne jest przechwycenie wartości hello hello dysków, obsługujące obciążenia aplikacji. W przypadku jedno mapowanie tooone między dysków logicznych i fizycznych, może się odwoływać toophysical liczniki; w przeciwnym razie można znaleźć toohello liczników dysku logicznego. W systemie Linux polecenie iostat hello generuje raport o wykorzystaniu Procesora i dysku. Raport o wykorzystaniu dysku Hello zawiera dane statystyczne na urządzeniu fizycznym lub partycji. Jeśli masz serwer bazy danych z danych i dziennika na oddzielnych dyskach zbierać dane dla obydwa dyski. Poniższej tabeli opisano liczniki dotyczące dysków, procesora i pamięci:

| Licznik | Opis | Monitora wydajności | Iostat |
| --- | --- | --- | --- |
| **Liczba IOPS lub transakcje na sekundę** |Liczba żądań We/Wy wystawiony toohello dysk magazynujący na sekundę. |Odczyty dysku/s <br> Zapisy dysku/s |tps <br> r/s <br> p/s |
| **Dysk odczyty i zapisy** |% operacji odczytu i zapisu operacji wykonywanych na powitania dysku. |Czas odczytu dysku (%) <br> Czas zapisu na dysku % |r/s <br> p/s |
| **Przepływność** |Ilość danych odczytu lub zapisu toohello dysku na sekundę. |Bajty odczytu dysku/s <br> Bajty zapisu dysku/s |kB_read/s <br> kB_wrtn/s |
| **Opóźnienie** |Całkowity czas toocomplete żądania We/Wy dysku. |Średnia dysku w s/Odczyt <br> Średnia dysku w s/Zapis |await <br> svctm |
| **Rozmiar operacji We/Wy** |rozmiar Hello żądań We/Wy wystawia toohello dysków w magazynie. |Bajty odczytu dysku <br> Bajty zapisu dysku |avgrq sz |
| **Głębokość kolejki** |Liczba oczekujących operacji We/Wy żądań toobe oczekiwania zapisu dysku magazynu toohello lub odczytu formularza. |Bieżąca długość kolejki dysku |avgqu sz |
| **Maks. Pamięci** |Ilość pamięci wymagana sprawnie toorun aplikacji |Zadeklarowane bajty w użyciu (%) |Użyj vmstat |
| **Maks. PROCESOR CPU** |Ilość Procesora wymaganej aplikacji toorun sprawnie |Czas procesora (%) |% util |

Dowiedz się więcej o [iostat](http://linuxcommand.org/man_pages/iostat1.html) i [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Optymalizacja wydajności aplikacji
Witaj główne czynniki wpływające na wydajność aplikacji uruchomionych na magazyn w warstwie Premium są charakter z żądania We/Wy, rozmiar maszyny Wirtualnej, rozmiar dysku, liczbę dysków, dysku pamięci podręcznej, Multithreading i głębokość kolejki. Niektóre z tych czynników można kontrolować z obsługiwanych przez hello system pokrętła. Większość aplikacji może nie zapewniają hello tooalter — opcja rozmiaru we/wy i głębokość kolejki bezpośrednio. Na przykład jeśli używasz programu SQL Server, nie można wybrać głębokość we/wy hello rozmiaru i kolejki. SQL Server wybiera hello optymalne we/wy rozmiaru i kolejki głębokość wartości tooget hello większości wydajności. Jest ważne toounderstand hello skutków obu typów czynników na wydajność aplikacji, dzięki czemu można udostępnić odpowiednie zasoby toomeet wydajności potrzeb.

W tej sekcji można znaleźć toohello aplikacji wymagania listę kontrolną, która została utworzona, tooidentify ile potrzebujesz toooptimize wydajność aplikacji. Na podstawie, będzie możliwe toodetermine które czynniki w tej sekcji możesz należy tootune. toowitness hello skutków każdy czynnik na aplikacji wydajność, uruchom przeprowadzenia testów porównawczych narzędzia w ustawieniach aplikacji. Zobacz toohello [Benchmarking](#Benchmarking) sekcji na końcu hello tego artykułu toorun kroki wspólne, przeprowadzenia testów porównawczych narzędzia w systemach Windows i maszyn wirtualnych systemu Linux.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>Optymalizacja IOPS, przepustowości i opóźnień w skrócie
w poniższej tabeli Hello podsumowanie wszystkich hello wydajności czynniki oraz hello kroki toooptimize IOPS, przepustowości i opóźnień. Witaj sekcjach poniżej to podsumowanie opisano każdy czynnik jest znacznie bardziej szczegółowo.

| &nbsp; | **IOPS** | **Przepływność** | **Opóźnienie** |
| --- | --- | --- | --- |
| **Przykładowy scenariusz** |Enterprise OLTP aplikacji wymagających bardzo duże transakcje na drugi szybkości. |Magazynowania aplikacji przetwarzania dużych ilości danych danych przedsiębiorstwa. |Niemal w czasie rzeczywistym aplikacji wymagających odpowiedzi błyskawicznych toouser żądań, takich jak gier online. |
| Czynniki wydajności | &nbsp; | &nbsp; | &nbsp; |
| **Rozmiar operacji We/Wy** |Mniejszego rozmiaru we/wy daje wyższa wartość IOPS. |Większe tooyields rozmiaru we/wy wyższej przepustowości. | &nbsp;|
| **Rozmiar maszyny Wirtualnej** |Użyj rozmiar maszyny Wirtualnej, który oferuje IOPS większą niż wymagań aplikacji. Zobacz rozmiarów maszyn wirtualnych i limity ich IOPS. |Rozmiar maszyny Wirtualnej za pomocą limit przepływności większy od wymagań aplikacji. Zobacz rozmiarów maszyn wirtualnych i limity ich przepływności. |Użyj rozmiar maszyny Wirtualnej, że oferty skalować limity większe wymagania Twojej aplikacji. Zobacz rozmiarów maszyn wirtualnych i limity ich tutaj. |
| **Rozmiar dysku** |Użyj rozmiar dysku, który oferuje IOPS większą niż wymagań aplikacji. Zobacz rozmiary dysków i limity ich IOPS. |Rozmiar dysku za pomocą limit przepływności większy od wymagań aplikacji. Zobacz rozmiary dysków i limity ich przepływności. |Użyj rozmiaru dysku, czy oferuje skalowanie limity większe wymagania Twojej aplikacji. Zobacz rozmiary dysków i limity ich tutaj. |
| **Maszyna wirtualna i limity skalowania dysku** |Wybrany rozmiar maszyny Wirtualnej hello limitu IOPS powinna być większa niż całkowita liczba IOPS regulowane przez dyski magazynu premium dołączony tooit. |Limit przepustowości wybrany rozmiar maszyny Wirtualnej hello powinna być większa niż całkowita przepływność regulowane przez dyski magazynu premium dołączony tooit. |Limity skalowania o wybrany rozmiar maszyny Wirtualnej hello musi być większa niż limity skalowania całkowita premium dołączonych dysków magazynowania. |
| **Buforowanie dysku** |Włącz pamięć podręczną tylko do odczytu na dyski magazynu premium z tooget duże operacje odczytu wyższej IOPS odczytu. | &nbsp; |Włącz pamięć podręczną tylko do odczytu na dyski magazynu premium z bardzo małych opóźnień odczytu gotowy duże operacje tooget. |
| **Rozkładanie** |Przy użyciu wielu dysków i paskowych je razem tooget Scalonej wyższa wartość IOPS i limit przepływności. Należy pamiętać, że hello łączny limit dla maszyny Wirtualnej powinna być większa niż hello łączne limity premium dołączonych dysków. | &nbsp; | &nbsp; |
| **Rozmiar usługi STRIPE** |Mniejszy rozmiar stripe dla losowych małych wzorca we/wy w aplikacji OLTP. Przykład dla aplikacji OLTP programu SQL Server za pomocą usługi stripe rozmiar 64KB. |Większy rozmiar stripe sequential dużych wzorzec we/wy w magazynie danych aplikacji. Np. Użyj rozmiaru stripe 256KB dla aplikacji magazynu danych programu SQL Server. | &nbsp; |
| **Wielowątkowość** |Użyj wielowątkowość toopush większej liczby żądań tooPremium magazynu, który prowadzi toohigher IOPS i przepustowość. Na przykład na serwerze SQL ustawić wysokiej tooallocate wartość MAXDOP więcej tooSQL procesorów serwera. | &nbsp; | &nbsp; |
| **Głębokość kolejki** |Głębokość kolejki większej daje wyższa wartość IOPS. |Głębokość kolejki większej daje wyższej przepustowości. |Mniejsze głębokość kolejki daje niższe opóźnienia. |

## <a name="nature-of-io-requests"></a>Rodzaj żądań We/Wy
Żądania We/Wy jest jednostką operacji wejścia/wyjścia, której aplikacja będzie wykonywać. Identyfikowanie hello rodzaj żądań We/Wy, losowych lub sekwencyjnych, odczytu lub zapisu, małych i dużych, pomoże określić wymagania dotyczące wydajności hello aplikacji. Jest bardzo ważne toounderstand hello rodzaj żądań We/Wy, toomake hello prawidłowych decyzji podczas projektowania infrastruktury aplikacji.

Rozmiar operacji We/Wy jest jednym z hello bardziej ważne czynniki. Witaj rozmiaru we/wy jest rozmiarem hello hello żądania operacji wejścia/wyjścia wygenerowane przez aplikację. Hello rozmiaru we/wy ma znaczący wpływ na wydajność, szczególnie w przypadku hello IOPS i przepustowości, jaką aplikacji hello jest tooachieve stanie. Witaj następująca formuła zawiera hello relacji między IOPS, rozmiaru we/wy i przepustowości/przepływności.  
    ![](media/storage-premium-storage-performance/image1.png)

Niektóre aplikacje pozwalają tooalter rozmiar ich we/wy, gdy niektóre aplikacje nie. Na przykład programu SQL Server określa hello optymalny we/wy rozmiar się i nie zapewnia użytkowników z dowolnego toochange pokrętła go. Na hello drugiej strony, Oracle zawiera parametr o nazwie [DB\_ZABLOKOWAĆ\_rozmiar](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) za pomocą którego można skonfigurować hello rozmiar żądania We/Wy hello bazy danych.

Jeśli używasz aplikacji, która nie zezwala na możesz toochange hello rozmiaru we/wy, użyj wytycznych hello tego artykułu toooptimize hello wydajność kluczowych wskaźników wydajności, który jest najbardziej odpowiednia aplikacja tooyour. Na przykład:

* Aplikacja OLTP generuje miliony małych i losowe żądań We/Wy. żąda toohandle te typu we/wy, należy zaprojektować tooget infrastruktury Twojej aplikacji wyższa wartość IOPS.  
* Aplikacja magazynowania danych generuje duży i kolejnych żądań We/Wy. toohandle te wpisz żądań We/Wy, należy zaprojektować tooget infrastruktury aplikacji większej przepustowości lub przepływności.

Jeśli używasz aplikacji, dzięki czemu rozmiar we/wy hello toochange, użyj tego zasadą dla hello we/wy dodatkowo rozmiaru tooother wskazówki dotyczące wydajności,

* Mniejsze tooget rozmiaru we/wy wyższa wartość IOPS. Na przykład 8 KB aplikacji OLTP.  
* Większe tooget rozmiaru we/wy wyższej przepustowości/przepustowości. Na przykład 1024 KB dla aplikacji magazynu danych.

Oto przykład na obliczenie hello IOPS i przepływności/przepustowość dla aplikacji. Należy wziąć pod uwagę przy użyciu dysku P30 aplikacji. Witaj maksymalna liczba IOPS i dysku P30 można osiągnąć przepływności/przepustowości jest 5000 IOPS i 200 MB na sekundę odpowiednio. Teraz Jeśli aplikacja wymaga hello maksymalna liczba IOPS z dysku hello P30 i użyć mniejszego rozmiaru we/wy, takich jak 8 KB hello wynikowa przepustowości będzie tooget możliwe jest 40 MB na sekundę. Jednak jeśli aplikacja wymaga hello maksymalnej przepływności/przepustowości z dysku P30 i używać większego rozmiaru we/wy, takich jak 1024 KB, hello IOPS wynikowy będzie mniejsza, 200 IOPS. W związku z tym dostroić hello rozmiaru we/wy, tak, że spełnia on wymagania IOPS i przepływności/przepustowość zarówno Twojej aplikacji. W poniższej tabeli przedstawiono dysku P30 hello różne rozmiary we/wy oraz ich odpowiednich IOPS i przepływności.

| Wymagania aplikacji | Rozmiar operacji We/Wy | Operacje wejścia/wyjścia | Przepływność/przepustowość |
| --- | --- | --- | --- |
| Maksymalna liczba IOPS |8 KB |5,000 |40 MB na sekundę |
| Przepustowość maksymalna |1024 KB |200 |200 MB / s |
| Maksymalna przepustowość + wysokiej IOPS |64 KB |3,200 |200 MB / s |
| Maksymalna liczba IOPS + wysokiej przepływności |32 KB. |5,000 |160 MB na sekundę |

tooget IOPS i przepustowości wyższa niż wartość maksymalna hello dysku magazynu premium w jednym używać wielu dysków w warstwie premium rozkładane razem. Na przykład paskowych dwóch tooget dysków P30 łączna liczba IOPS z 10 000 IOPS lub łączna przepustowość 400 MB na sekundę. Zgodnie z objaśnieniem w następnej sekcji hello, musisz użyć rozmiaru maszyny Wirtualnej, obsługującego dysku hello łączyć IOPS i przepływności.

> [!NOTE]
> Jak zwiększyć albo IOPS lub przepływności hello innych zwiększa się również, upewnij się, że nie naciśnięciu przepływności lub limity liczby hello dysku lub maszyny Wirtualnej podczas zwiększenie dowolnego z nich.
>
>

toowitness hello skutków rozmiaru we/wy na wydajność aplikacji, można uruchomić narzędzia najlepszymi na maszyny Wirtualnej i dysków. Tworzenie wielu uruchomień testów i użyj innego rozmiaru we/wy dla każdego wpływ hello toosee wykonywania. Zobacz toohello [Benchmarking](#Benchmarking) sekcji na końcu hello w tym artykule, aby uzyskać więcej informacji.

## <a name="high-scale-vm-sizes"></a>Wysoka skalowalność rozmiarów maszyn wirtualnych
Po ponownym uruchomieniu, projektowania aplikacji, co pierwszy toodo rzeczy hello jest, wybierz toohost maszyny Wirtualnej aplikacji. Magazyn w warstwie Premium jest dostarczany z rozmiary wysokiej skali maszyny Wirtualnej, które można uruchomić aplikacji wymagających wyższej moc obliczeniową i wysokiej wydajności We/Wy dysku lokalnym. Te maszyny wirtualne zapewniają szybkich procesorów, większy współczynnik pamięci — podstawowe i Solid-State Drive (SSD) dla dysku lokalne powitania. Przykłady wysokiej skali maszyny wirtualne obsługujące magazyn w warstwie Premium hello DS, DSv2 i GS serii maszyn wirtualnych.

Wysokiej skali maszyny wirtualne są dostępne w różnych rozmiarach z różną liczbę rdzeni Procesora, pamięci, systemu operacyjnego i rozmiar dysku tymczasowym. Rozmiar każdej maszyny Wirtualnej ma również maksymalna liczba dysków danych dołączenie toohello maszyny Wirtualnej. W związku z tym hello wybrany rozmiar maszyny Wirtualnej będzie miało wpływ na pojemność przydzielaną przetwarzania, pamięci oraz Magazyn jest dostępny dla twojej aplikacji. Dotyczy również hello obliczeniowych i przestrzeni magazynowej. Na przykład poniżej przedstawiono specyfikacje hello hello największy rozmiar maszyny Wirtualnej w serii DS, DSv2 serii i serii GS:

| Rozmiar maszyny wirtualnej | Rdzenie procesora CPU | Memory (Pamięć) | Rozmiary dysków maszyny Wirtualnej | Maksymalnie z Dyski danych | Rozmiar pamięci podręcznej | Operacje wejścia/wyjścia | Limity przepustowości we/wy w pamięci podręcznej |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS14 |16 |112 GB |SYSTEM OPERACYJNY = 1023 GB. <br> Lokalny dysk SSD = 224 GB |32 |576 GB |50 000 IOPS <br> 512 MB na sekundę |4000 IOPS i 33 MB na sekundę |
| Standard_GS5 |32 |448 GB |SYSTEM OPERACYJNY = 1023 GB. <br> Lokalny dysk SSD = 896 GB |64 |4224 GB |80 000 IOPS <br> 2000 MB na sekundę |5000 IOPS i 50 MB / s |

tooview pełną listę wszystkich dostępnych rozmiarów maszyny Wirtualnej platformy Azure można znaleźć zbyt[rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [rozmiarów maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Wybierz rozmiar maszyny Wirtualnej, które mogą zaspokoić i skali tooyour potrzeby wymagania dotyczące wydajności aplikacji. Ponadto toothis, uwzględniać następujące istotne kwestie, wybierając rozmiarów maszyn wirtualnych.

*Limity skalowania*  
Hello maksymalną wartością IOPS dla poszczególnych maszyn wirtualnych i dysk są różne i od siebie niezależne. Upewnij się, że aplikacja hello sterujące IOPS w granicach hello hello maszyny Wirtualnej, a także tooit dołączonych dysków premium hello. W przeciwnym razie wydajności aplikacji może wystąpić ograniczenie.

Na przykład załóżmy, że wymagania aplikacji jest maksymalnie 4000 IOPS. tooachieve P30 dysku na maszynie Wirtualnej DS1, należy udostępnić. Witaj P30 dysku może dostarczać too5, 000 IOPS. Hello DS1 maszyna wirtualna jest jednak ograniczona too3, 200 IOPS. W rezultacie wydajność aplikacji hello będzie ograniczone przez hello wirtualna limitu 3,200 IOPS i będzie pogorszenie wydajności. tooprevent tej sytuacji, wybierz Maszynę wirtualną, a rozmiar, który będzie zarówno aplikacji spełniają wymagania dotyczące dysku.

*Koszt operacji*  
W wielu przypadkach istnieje możliwość, że Twoje całkowity koszt operację przy użyciu magazyn w warstwie Premium jest niższa niż przy użyciu magazynu w warstwie standardowa.

Rozważmy na przykład aplikacji wymagających 16 000 IOPS. tooachieve to wydajność, konieczne będzie Standard\_D14 IaaS maszyny Wirtualnej platformy Azure, której można nadać maksymalną liczbę IOPS 16000 przy użyciu 32 dyskach 1 TB magazynu w warstwie standardowa. Każdy dysk magazynu w warstwie standardowa 1TB, można osiągnąć maksymalnie 500 IOPS. Witaj szacowany koszt tej maszyny Wirtualnej na miesiąc będą 1,570 $. miesięczny koszt Hello 32 dyski magazynu w warstwie standardowa będzie 1,638 $. Witaj szacowany całkowity miesięczny koszt będzie 3,208 $.

Jednak jeśli użytkownik jest hostowany hello sama aplikacja na magazyn w warstwie Premium, konieczne będzie mniejszego rozmiaru maszyny Wirtualnej i mniej dyski magazynu premium, co zmniejsza całkowity koszt hello. Standard\_DS13 maszyny Wirtualnej można wymaganie hello 16000 IOPS za pomocą czterech P30 dysków. Hello DS13 maszyny Wirtualnej ma maksymalne IOPS 25,600, a każdy dysk P30 ma maksymalne IOPS 5000. Ogólne, ta konfiguracja może osiągnąć 5000 x 4 = 20 000 IOPS. Witaj szacowany koszt tej maszyny Wirtualnej na miesiąc będą 1,003 $. miesięczny koszt cztery dyski magazynu premium P30 Hello będzie 544.34 $. Witaj szacowany całkowity miesięczny koszt będzie 1,544 $.

W poniższej tabeli przedstawiono podziału kosztów hello tego scenariusza Standard i Premium Storage.

| &nbsp; | **Standardowa** | **Premium** |
| --- | --- | --- |
| **Koszt maszyny wirtualnej na miesiąc** |1,570.58 $ (standardowa\_D14) |1,003.66 $ (standardowa\_DS13) |
| **Koszt dysków na miesiąc** |$1,638.40 (dyski 32 x 1 TB) |$544.34 (4 dyski x P30) |
| **Całkowity koszt na miesiąc** |$3,208.98 |$1,544.34 |

*Dystrybucjach systemu Linux*  

Usługa Azure Premium Storage, możesz uzyskać hello tego samego poziomu wydajności dla maszyn wirtualnych z systemem Windows i Linux. Firma Microsoft obsługuje wiele odmian dystrybucjach systemu Linux, aby zobaczyć pełną listę hello [tutaj](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Jest ważne, toonote czy różnych dystrybucjach są lepiej dopasowane do różnych rodzajów obciążeń. Zostanie wyświetlone różne poziomy wydajności w zależności od distro hello, obciążenie na którym działa. Testowanie hello dystrybucjach systemu Linux z aplikacją, a następnie wybierz hello, który najlepiej.

Podczas uruchamiania systemu Linux z magazyn w warstwie Premium, Sprawdź najnowsze aktualizacje hello o wysokiej wydajności tooensure wymagane sterowniki.

## <a name="premium-storage-disk-sizes"></a>Rozmiary dysków Premium magazynu
Usługa Azure Premium Storage oferuje obecnie siedem rozmiary dysków. Rozmiar każdego dysku ma limit innej skali IOPS, przepustowości i magazynu. Wybieranie właściwego rozmiaru dysku magazynu Premium hello w zależności od wymagań aplikacji hello i hello dużą skalę rozmiaru maszyny Wirtualnej. Witaj w poniższej tabeli przedstawiono hello siedmiu dysków rozmiary i ich funkcji. Rozmiary P4 i P6 są obecnie obsługiwane tylko w przypadku zarządzania dyskami.

| Typ dysków Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Rozmiar dysku           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Przepływność na dysk | 25 MB na sekundę  | 50 MB / s  | 100 MB na sekundę | 150 MB na sekundę | 200 MB / s | 250 MB na sekundę | 250 MB na sekundę | 


Jak wiele dysków, możesz wybrać, zależy od hello na dysku wybranego rozmiaru. Można użyć jednego dysku P50 lub wielu toomeet dysków P10 wymagań aplikacji. Należy uwzględnić wymienione poniżej podczas wprowadzania wybór hello uwagi dotyczące konta.

*Limity skalowania (IOPS i przepustowości)*  
limitu IOPS i przepływność Hello rozmiar każdego dysku Premium jest inna i niezależne od limity skalowania maszyny Wirtualnej hello. Upewnij się, że hello łączna liczba IOPS i przepływność z hello dysków w ramach limitów skalowania hello wybrano rozmiar maszyny Wirtualnej.

Na przykład, jeśli wymagania aplikacji jest maksymalnie 250 MB/s przepustowości i DS4 maszyny Wirtualnej za pomocą jednego dysku P30. Witaj DS4 maszyny Wirtualnej można zrezygnować too256 MB/s przepustowości. Jednak jeden dysk P30 ma limit przepustowości 200 MB/s. W rezultacie aplikacji hello będą ograniczone na 200 MB/s, ze względu na ograniczenia toohello na dysku. tooovercome ten limit, udostępnić więcej niż jeden toohello dysków danych maszyny Wirtualnej lub zmiany rozmiaru programu tooP40 dysków lub P50.

> [!NOTE]
> Odczyty obsłużone przez pamięć podręczną hello nie znajdują się w dysku hello IOPS i przepustowość, więc nie podmiotu toodisk limity. Pamięć podręczna ma oddzielne IOPS i przepływność limit dla maszyny Wirtualnej.
>
> Na przykład początkowo Twojej odczyty i zapisy są 60MB/s i 40MB/s odpowiednio. Wraz z upływem czasu pamięci podręcznej hello warms i służy coraz większą hello odczyty z pamięci podręcznej hello. Następnie możesz uzyskać zapisu wyższej przepustowości z hello dysku.
>
>

*Liczba dysków*  
Określ numer hello dysków, które mają być przez proces oceny wymagań aplikacji. Rozmiar każdej maszyny Wirtualnej ma również limit hello liczby dysków dołączenie toohello maszyny Wirtualnej. Zazwyczaj jest to dwa razy hello liczby rdzeni. Upewnij się, tym hello rozmiar maszyny Wirtualnej, wybrane może obsługiwać hello liczbę dysków potrzebne.

Należy pamiętać, że hello magazyn w warstwie Premium dyski mają wyższe wydajności możliwości w porównaniu tooStandard dysków w magazynie. W związku z tym aplikacji w przypadku migracji z maszyn wirtualnych IaaS platformy Azure za pomocą magazynu w warstwie standardowa tooPremium magazynu, potrzebne będą prawdopodobnie mniej dysków premium tooachieve hello takiej samej lub wyższej wydajności aplikacji.

## <a name="disk-caching"></a>Buforowanie dysku
Wysoka maszyn wirtualnych skali, korzystających z usługi Azure Premium Storage jest wielowarstwowych technologii buforowania, nazywany BlobCache. BlobCache korzysta z kombinacji hello maszyny wirtualnej ilość pamięci RAM i lokalny dysk SSD dla buforowania. Ta pamięć podręczna jest dostępny na dyski stałe hello magazyn w warstwie Premium i dyski lokalne powitania maszyny Wirtualnej. Domyślnie to ustawienie pamięci podręcznej ma wartość tooRead/zapisu dla dysków systemu operacyjnego i tylko do odczytu dla dysków z danymi hostowanych na magazyn w warstwie Premium. Z dysku Buforowanie włączone na dyskach magazyn w warstwie Premium hello, wysokiej skali hello maszyn wirtualnych można osiągnąć bardzo wysoki poziom wydajności, które przekraczają hello podstawowej wydajności dysku.

> [!WARNING]
> Zmiany ustawień pamięci podręcznej hello Azure dysku odłącza i dołącza ponownie hello dysk docelowy. Jeśli jest dysk systemu operacyjnego hello hello maszyny Wirtualnej jest uruchamiany ponownie. Zatrzymaj wszystkie aplikacji/usługi, które mogą wpłynąć na przerw w działaniu w przed zmianą ustawienie hello dyskowej pamięci podręcznej.
>
>

toolearn więcej informacji na temat działania BlobCache można znaleźć toohello wewnątrz [Azure Premium Storage](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) wpis w blogu.

Jest ważne tooenable pamięci podręcznej hello prawidłowego zestawu dysków. Określa, czy należy włączyć buforowanie dysku na dysku premium lub nie będzie zależeć od wzorzec obciążenia hello tego dysku będą obsługi. Poniższa tabela zawiera hello domyślnego ustawienia pamięci podręcznej dla systemu operacyjnego i dysków z danymi.

| **Typ dysku** | **Domyślne ustawienie pamięci podręcznej** |
| --- | --- |
| Dysk systemu operacyjnego |ReadWrite |
| Dysk z danymi |Brak |

Poniżej są hello ustawienia pamięci podręcznej dysku zalecane dla dysków z danymi

| **Ustawienia buforowania na dysku** | **Zalecenie o tym, kiedy toouse tego ustawienia** |
| --- | --- |
| Brak |Konfigurowanie hosta pamięci podręcznej None tylko do zapisu i intensywnie zapisu dysków. |
| Tylko do odczytu |Skonfiguruj pamięci podręcznej hosta jako tylko do odczytu dla dysków tylko do odczytu i zapisu i odczytu. |
| ReadWrite |Konfigurowanie pamięci podręcznej hosta jako ReadWrite tylko wtedy, gdy aplikacja obsługuje prawidłowo, zapisywanie w pamięci podręcznej danych toopersistent dyski w razie potrzeby. |

*Tylko do odczytu*  
Konfigurując buforowanie danych magazyn w warstwie Premium dyski tylko do odczytu, możesz osiągnąć Niskie opóźnienie odczytu i uzyskać bardzo duże IOPS odczytu i przepływność aplikacji. Jest to powodu dwóch przyczyn

1. Odczyty wykonywane z pamięci podręcznej, która znajduje się na powitania pamięci maszyny Wirtualnej i lokalny dysk SSD, jest znacznie szybsze niż odczyty hello dysk danych, który znajduje się na powitania magazynu obiektów blob platformy Azure.  
2. Magazyn w warstwie Premium nie będą uwzględniane hello obsłużone odczyty z pamięci podręcznej dysku hello IOPS i przepływności. W związku z tym aplikacja jest możliwe tooachieve wyższe łączna liczba IOPS i przepustowość.

*ReadWrite*  
Domyślnie hello dysków systemu operacyjnego mają włączone buforowanie odczytu i zapisu. Niedawno dodano obsługę ReadWrite buforowanie na danych, jak również dysków. Jeśli korzystasz z buforowaniem odczytu i zapisu, muszą mieć właściwy sposób toowrite hello danych z pamięci podręcznej toopersistent dysków. Na przykład dojść programu SQL Server do zapisywania buforowane dysków z danymi toohello magazynu trwałego samodzielnie. Przy użyciu pamięci podręcznej odczytu i zapisu z aplikacją, która nie obsługuje trwałych hello wymaganych danych może spowodować utratę toodata, jeśli wystąpiła awaria hello maszyny Wirtualnej.

Na przykład można zastosować te wytyczne tooSQL serwera uruchomionych na magazyn w warstwie Premium, wykonując poniższe polecenie hello,

1. Konfigurowanie pamięci podręcznej "ReadOnly" premium magazynu dysków zawierających pliki danych.  
   a.  Hello szybkiego odczytuje z czas kwerendy SQL Server niższe hello pamięci podręcznej, ponieważ dane strony są znacznie szybciej pobierane z hello toodirectly pamięci podręcznej w porównaniu z dysków z danymi hello.  
   b.  Obsługująca odczyty z pamięci podręcznej, oznacza, że jest dostępny z dysków danych w warstwie premium dodatkowej przepływności. SQL Server można korzystać tego dodatkowe przepływności kierunku pobieranie więcej danych stron i inne operacje, takie jak Kopia zapasowa i przywracanie, partii obciążeń i spowoduje odbudowanie indeksu.  
2. Skonfiguruj "None" hostingu plików dziennika hello dyski pamięci podręcznej na magazyn w warstwie premium.  
   a.  Pliki dziennika mają głównie operacje zapisu ciężki. W związku z tym ich nie korzystają z hello pamięci podręcznej tylko do odczytu.

## <a name="disk-striping"></a>Rozkładanie
Gdy wysoką skalowalność, której maszyna wirtualna jest dołączona z kilku magazynu trwałego dysków premium hello dysków może być rozłożone razem tooaggregate w ich IOPs, przepustowości i pojemności magazynu.

W systemie Windows można używać funkcji miejsca do magazynowania dysków toostripe ze sobą. Należy skonfigurować jedną kolumnę dla każdego dysku w puli. W przeciwnym razie hello ogólną wydajność woluminów rozłożonych może być niższe niż oczekiwano powodu dystrybucji toouneven ruchu na dyskach hello.

Ważne: Przy użyciu interfejsu użytkownika Menedżera serwera, można ustawić hello łączna liczba kolumn w górę too8 dla woluminy rozłożone. Podczas podłączania więcej niż 8 dysków, korzystają z woluminu hello toocreate środowiska PowerShell. Przy użyciu programu PowerShell, można ustawić hello liczbę kolumn równy toohello liczba dysków. Na przykład, jeśli istnieją 16 dysków w jednej rozłożony; Określ 16 kolumn w hello *NumberOfColumns* parametru hello *New-VirtualDisk* polecenia cmdlet programu PowerShell.

W systemie Linux użyć hello MDADM narzędzie toostripe dysków. Aby uzyskać szczegółowy opis kroków na dyskach zastosowanie rozkładania na systemie Linux, zobacz zbyt[skonfigurować RAID oprogramowania w systemie Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Rozmiar usługi STRIPE*  
Ważne konfiguracji w rozkładanie jest hello rozmiar przeplotu. rozmiar przeplotu Hello lub rozmiar bloku jest hello najmniejszą fragmentów danych aplikacji można rozwiązać na woluminy rozłożone. rozmiar przeplotu Hello skonfigurowanych zależy od typu hello aplikacji i jej wzorzec żądania. Jeśli wybierzesz hello stripe niewłaściwy rozmiar spowodować niespójność tooIO, co prowadzi toodegraded wydajność aplikacji.

Na przykład jeśli żądanie We/Wy wygenerowanych przez aplikację jest większy niż rozmiar stripe dysku hello, hello magazynu systemu zapisuje go na stripe granice jednostki na więcej niż jeden dysk. Gdy jest on czasu tooaccess danych, jej tooseek przez więcej niż jedno żądanie hello toocomplete jednostki usługi stripe. Hello skrócenie takie zachowanie może spowodować spadek wydajności toosubstantial. Na powitania drugiej strony, jeśli hello rozmiar żądania We/Wy jest mniejszy niż rozmiar stripe i jeśli charakter losowy, żądań We/Wy hello może sumują na powitania takie same dysku przyczyną wąskiego gardła i ostatecznie zmniejszenie wydajności we/wy hello.

W zależności od typu hello obciążenia aplikacja jest uruchomiona, wybierz odpowiednie stripe rozmiar. Losowe małych żądań We/Wy Użyj mniejszej stripe. Dla dużych sekwencyjnych operacji We/Wy żądań stosować większy rozmiar przeplotu. Dowiedz się hello stripe rozmiar zalecenia dotyczące aplikacji hello się, że będzie działać na magazyn w warstwie Premium. Dla programu SQL Server należy skonfigurować usługi stripe rozmiarze 64KB dla obciążeń OLTP i 256KB dla obciążeń magazynowania danych. Zobacz [wydajności najlepsze rozwiązania dotyczące programu SQL Server na maszynach wirtualnych Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn więcej.

> [!NOTE]
> Jednocześnie można możesz paskowych maksymalnie 32 dyski magazynu premium na serii DS maszyny Wirtualnej i 64 dyski magazynu premium na serię GS maszyny Wirtualnej.
>
>

## <a name="multi-threading"></a>Wielowątkowości
Azure zostało zaprojektowane, równoległemu toobe platformy magazyn w warstwie Premium. W związku z tym aplikacji wielowątkowych osiąga o wiele większą wydajność niż jednowątkowe aplikacji. Aplikacji wielowątkowych podzieli zadań przez wiele wątków i zwiększa efektywność działania za pomocą hello maszyny Wirtualnej i maksymalną toohello zasobów dysku.

Na przykład jeśli aplikacja jest uruchomiona na jednym rdzeniu maszyny Wirtualnej przy użyciu dwóch wątków, hello procesora CPU można przełączać się między hello dwoma wątkami tooachieve wydajności. Gdy jeden wątek oczekuje na toocomplete We/Wy dysku, hello procesora CPU można przełączać toohello innego wątku. W ten sposób dwoma wątkami można wykonywać więcej niż jednego wątku czy. Jeśli hello maszyna wirtualna ma więcej niż jednego rdzenia, dalsze zmniejsza czas działania, ponieważ każdy core mogą wykonywać zadania równolegle.

Nie może być sposób hello stanie toochange standardowych aplikacji implementuje pojedynczego wątku lub wielowątkowości. Na przykład SQL Server jest może obsługiwać wielu procesorów i procesorami wielordzeniowymi. Jednak program SQL Server decyduje, pod jakimi warunkami będzie korzystać jeden lub więcej wątków tooprocess zapytania. Można go uruchamiać zapytania i tworzą indeksy, używając wielowątkowości. Dla zapytania, które obejmuje przyłączanie dużych tabel i sortowanie danych przed zwróceniem toohello użytkownika wiele wątków prawdopodobnie będzie używany przez serwer SQL. Jednak użytkownik nie może kontrolować, czy program SQL Server wykonuje zapytanie za pomocą pojedynczego wątku lub wiele wątków.

Brak ustawienia konfiguracji, możliwość zmiany tooinfluence tym wielowątkowości lub równoległego przetwarzania aplikacji. Na przykład w przypadku programu SQL Server jest hello maksymalny stopień równoległości konfiguracji. To ustawienie o nazwie MAXDOP, pozwala tooconfigure hello maksymalną liczbę procesorów, które program SQL Server można użyć podczas przetwarzania równoległe. MAXDOP można skonfigurować dla poszczególnych zapytań lub operacji dotyczących indeksu. Jest to przydatne, gdy ma toobalance zasoby systemu dla aplikacji krytyczne wydajności.

Na przykład aplikację za pomocą programu SQL Server jest wykonywany dużych zapytań i operacji indeksowania na powitania tym samym czasie. Załóżmy chciał toobe operacja indeksu hello więcej zapytania dużych toohello wydajność w porównaniu. W takim przypadku można ustawić wartości MAXDOP hello indeksu operacji toobe wyższe niż hello MAXDOP wartość hello zapytania. Dzięki temu program SQL Server ma więcej liczbę procesorów, które można wykorzystać hello indeksu operacji porównaniu toohello liczbę procesorów, można go przypisać toohello dużych zapytania. Należy pamiętać, że nie kontroli hello liczba wątków, który będzie używany przez serwer SQL dla każdej operacji. Można kontrolować hello maksymalną liczbę procesorów jest przeznaczony dla wielowątkowości.

Dowiedz się więcej o [stopni równoległości](https://technet.microsoft.com/library/ms188611.aspx) w programie SQL Server. Dowiedz się takie ustawienia wpływające na wielowątkowości w aplikacji i ich wydajności toooptimize konfiguracji.

## <a name="queue-depth"></a>Głębokość kolejki
Witaj głębokość kolejki lub długość kolejki lub rozmiar kolejki jest hello liczba oczekujących żądań We/Wy w systemie hello. wartość Hello głębokość kolejki określa, ile operacji We/Wy aplikacji można wyrównać, które dyski magazynu hello będzie przetwarzania. Ma wpływ na wszystkie hello trzy aplikacji wskaźników wydajności, których wspomniano w tym tj artykułu IOPS, przepustowości i opóźnień.

Kolejka głębokość i wielowątkowości są ściśle powiązane. głębokość kolejki Hello wskazuje, ile wielowątkowości może osiągnąć aplikacji hello. W przypadku dużych hello głębokości kolejki, aplikacja może zostać uruchomiony więcej operacji jednocześnie, innymi słowy, więcej wielowątkowości. Jeśli hello głębokość kolejki jest mały, nawet jeśli aplikacja jest wielowątkowych, nie będzie wystarczającej liczby żądań wyrównana równoczesne wykonywanie.

Zazwyczaj poza hello półki aplikacje nie zezwalają toochange hello głębokości kolejki, ponieważ jeśli ustawione niepoprawnie czy obrażeniami więcej niż dobra. Aplikacje ustawi wartość prawej strony hello kolejki głębokość tooget hello optymalnej wydajności. Jednak on jest ważne toounderstand koncepcji, dzięki czemu można rozwiązywać problemy z wydajnością z aplikacją. Można również obserwować hello skutków głębokość kolejki przez uruchomienie narzędzia najlepszymi w systemie.

Niektóre aplikacje Podaj ustawienia tooinfluence hello głębokość kolejki. Na przykład hello MAXDOP (maksymalny stopień równoległości) ustawienie w programie SQL Server szczegółowo opisane w poprzedniej sekcji. MAXDOP jest sposób tooinfluence głębokość kolejki i wielowątkowości, chociaż nie zmienia bezpośrednio hello wartość głębokość kolejki programu SQL Server.

*Głębokość kolejki wysoka*  
Głębokość kolejki wysokiej linii więcej operacji na powitania dysku. dysk Hello wie hello następnego żądania w kolejce jego wcześniejsze. W związku z tym hello dysku można zaplanować operacji wcześniejsze i przetwarzanie ich w optymalny sekwencji. Ponieważ aplikacja hello wysyła więcej żądań toohello dysku, dysku hello może przetwarzać więcej równolegle z systemem IOs. Ostatecznie, aplikacja hello będzie możliwe tooachieve wyższa wartość IOPS. Ponieważ przetwarzanie żądań więcej aplikacji hello całkowitą przepływność aplikacji hello zwiększa także.

Zazwyczaj aplikacji można uzyskać maksymalną przepływność z 8-16 oczekujących operacji We-Wy na dysku dołączonym. Jeśli głębokości kolejki, aplikacja nie jest wypychanie za mało w systemie IOs toohello i przetworzy mniejszej ilości w danym okresie. Innymi słowy mniejszej przepustowości.

Na przykład w programie SQL Server, ustawienie hello MAXDOP wartość dla zapytania zbyt "4" informuje programu SQL Server można użyć toofour rdzeni tooexecute hello kwerendy. Programu SQL Server określa, co jest najlepszym kolejki głębokość wartość i hello liczba rdzeni w celu wykonywania zapytań hello.

*Optymalną głębokość kolejki*  
Głębokość kolejki bardzo duże ma również jego wady. Jeśli głębokość kolejki jest zbyt wysoka, aplikacja hello spróbuje toodrive bardzo wysoka liczba IOPS. Jeśli aplikacja ma trwały dysków o wystarczające elastycznie IOPS, to negatywnie wpłynąć na opóźnienia aplikacji. Następującej formuły przedstawiono relacje hello IOPS, opóźnienia i głębokość kolejki.  
    ![](media/storage-premium-storage-performance/image6.png)

Nie należy konfigurować głębokość kolejki tooany wysokiej wartości, ale wartość optymalną tooan, który może dostarczyć wystarczającej liczby IOPS dla aplikacji hello bez wpływu na opóźnienia. Na przykład jeśli opóźnienie aplikacji hello musi toobe 1 milisekund, hello głębokość kolejki wymagane jest 5000 IOPS, tooachieve QD = 5000 x 0,001 = 5.

*Głębokość kolejki dla woluminów rozłożonych*  
Dla woluminu rozłożonego Obsługa głębokości kolejki wystarczająco wysoka, tak, aby każdy dysk miała głębokość kolejki szczytu pojedynczo. Rozważmy na przykład aplikacja, który wypycha głębokości kolejki wynoszącej 2 i istnieją 4 dyski w hello stripe. Witaj dwie żądań We/Wy przejdzie tootwo dysków i pozostałych dwóch dysków będzie bezczynności. W związku z tym skonfigurować hello głębokość kolejki w taki sposób, że wszystkie dyski hello może być zajęta. Formuła poniżej pokazano, jak toodetermine hello głębokości kolejki wynoszącej woluminy rozłożone.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Ograniczanie przepływności
Azure Premium Storage przepisy określona liczba IOPS i Przepływność w zależności od hello rozmiarów maszyn wirtualnych i rozmiary dysków, którą wybierzesz. W dowolnym momencie aplikacja podejmie próbę toodrive IOPS lub przepływności powyżej tych limitów jakie hello maszyny Wirtualnej lub dysku może obsłużyć, będzie ograniczane przez Magazyn w warstwie Premium. To manifesty w formie hello pogorszenie wydajności w aplikacji. To oznacza większego opóźnienia, zmniejszenia przepustowości lub zmniejszyć liczbę IOPS. Jeśli magazyn w warstwie Premium nie ograniczenie przepustowości, aplikacji całkowicie może zakończyć się niepowodzeniem przekroczenia co jej zasoby są w stanie realizacji. Tak, z powodu problemów wydajności tooavoid toothrottling, zawsze należy zasoby odpowiednie do aplikacji. Wziąć pod uwagę, omówiono w sekcji rozmiary dysku powyżej i hello rozmiarów maszyn wirtualnych. Przeprowadzenia testów porównawczych jest hello najlepsze sposób toofigure limit zasobów, konieczne będzie toohost aplikacji.

## <a name="benchmarking"></a>Przeprowadzenia testów porównawczych
Przeprowadzenia testów porównawczych, to proces hello symulowanie różnych obciążeń w swojej aplikacji i pomiaru wydajności aplikacji hello dla poszczególnych obciążeń. Hello opisane w sekcji wcześniej zostały zebrane wymagania dotyczące wydajności aplikacji hello. Uruchamiając przeprowadzenia testów porównawczych narzędzia na maszynach wirtualnych hello hosting aplikacji hello, można określić hello poziomów wydajności, które aplikacji można uzyskać z magazyn w warstwie Premium. W tej sekcji możemy umożliwiają przykłady przeprowadzenia testów porównawczych standardowa maszyna VM DS14 udostępniane z dysków Azure Premium Storage.

Odpowiednio użyliśmy najlepszymi narzędziom Iometer i FIO, systemu Windows i Linux. Te narzędzia zduplikować wiele wątków symulując produkcji, takich jak obciążenia i wydajność systemu hello miary. Za pomocą narzędzi hello można również skonfigurować parametry, takie jak głębokość bloku rozmiar i kolejki, które normalnie nie można zmienić dla aplikacji. Zapewnia to większą elastyczność toodrive hello maksymalną wydajność na dużą skalę udostępniane z dysków w warstwie premium dla różnych typów aplikacji obciążeń maszyny Wirtualnej. można znaleźć więcej informacji na temat narzędzia najlepszymi toolearn [Iometer](http://www.iometer.org/) i [FIO](http://freecode.com/projects/fio).

Przykłady hello toofollow poniżej, utworzyć Maszynę wirtualną DS14 standardowe i Dołącz 11 magazyn w warstwie Premium toohello dysków maszyny Wirtualnej. Hello 11 dysków skonfiguruj 10 dysków z buforowania jako "None" na hoście, a paskowych je na wolumin o nazwie NoCacheWrites. Konfigurowanie buforowania jako "ReadOnly" hello pozostałych dysku hosta i Utwórz wolumin o nazwie CacheReads z tego dysku. Przy użyciu tej konfiguracji, będzie toosee stanie hello maksymalną odczytu i zapisu wydajności z standardowe DS14 maszyny Wirtualnej. Aby uzyskać szczegółowe instrukcje dotyczące tworzenia maszyny Wirtualnej DS14 z dysków w warstwie premium, przejdź zbyt[tworzenie i używanie konta magazynu Premium dla dysku danych maszyny wirtualnej](storage-premium-storage.md).

*Wstępne wypełnianie hello pamięci podręcznej*  
dysk Hello z buforowania na hoście tylko do odczytu będzie możliwe toogive IOPS wyższe niż limit hello na dysku. tooget Maksymalna wydajność odczytu z pamięci podręcznej hosta hello, najpierw należy rozgrzewki pamięci podręcznej hello tego dysku. Dzięki temu tego hello IOs odczytu najlepszymi narzędzie, które będą miały na woluminie CacheReads faktycznie trafienia pamięci podręcznej hello i nie hello dysku bezpośrednio. wynik trafień w pamięci podręcznej Hello dodatkowe IOPS z pamięci podręcznej pojedynczego hello włączone dysku.

> **Ważne:**  
> Przed uruchomieniem przeprowadzenia testów porównawczych, za każdym razem, gdy ponownego uruchomienia maszyny Wirtualnej musi rozgrzewki hello pamięci podręcznej.
>
>

#### <a name="iometer"></a>Iometer
[Pobierz narzędzie Iometer hello](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) na powitania maszyny Wirtualnej.

*Plik testowy*  
Iometer używa plik testu, który jest przechowywana w woluminie hello, na którym będzie uruchomiona hello przeprowadzenia testów porównawczych testu. Go dyski odczyty i zapisy na ten test dysku z plikiem toomeasure hello IOPS i przepustowość. Iometer tworzy ten plik testu, jeśli nie podano jeden. Utwórz plik testu 200GB o nazwie iobw.tst na powitania CacheReads i NoCacheWrites woluminów.

*Specyfikacje dostępu*  
Witaj specyfikacji, żądań We/Wy rozmiar % odczytu/zapisu, % losowe/sekwencyjne są konfigurowane za pomocą karty "Specyfikacje dostępu" hello w Iometer. Specyfikacja dostępu tworzone dla poszczególnych scenariuszy hello opisane poniżej. Tworzenie hello specyfikacje dostępu i przycisk Zapisz, odpowiedni nazywanie jak — RandomWrites\_8 kilobajtów RandomReads\_8 kilobajtów. Wybierz odpowiednie specyfikacji hello podczas uruchamiania hello scenariusza testu.

Przykład dostępu specyfikacji maksymalne IOPS zapisu scenariusz przedstawiono poniżej,  
    ![](media/storage-premium-storage-performance/image8.png)

*Maksymalna liczba IOPS specyfikacje testu*  
toodemonstrate maksymalne IOPs, użyj mniejszy rozmiar żądania. Użyj rozmiar żądania 8 KB i Utwórz specyfikacje zapisów losowych i odczytów.

| Specyfikacja dostępu | Rozmiar żądania | Losowe % | % Odczytu |
| --- | --- | --- | --- |
| RandomWrites\_8 kilobajtów |8 KB |100 |0 |
| RandomReads\_8 kilobajtów |8 KB |100 |100 |

*Maksymalna przepustowość specyfikacje testu*  
toodemonstrate maksymalną przepustowość, użyj większy rozmiar żądania. Użyj 64 KB rozmiaru żądania i Utwórz specyfikacje zapisów losowych i odczytów.

| Specyfikacja dostępu | Rozmiar żądania | Losowe % | % Odczytu |
| --- | --- | --- | --- |
| RandomWrites\_64 KB |64K |100 |0 |
| RandomReads\_64 KB |64K |100 |100 |

*Uruchomiona hello Iometer testu*  
Wykonaj kroki hello poniżej toowarm się pamięci podręcznej

1. Utwórz dwa specyfikacje dostępu z wartościami pokazano poniżej,

   | Nazwa | Rozmiar żądania | Losowe % | % Odczytu |
   | --- | --- | --- | --- |
   | RandomWrites\_1 MB |1MB |100 |0 |
   | RandomReads\_1 MB |1MB |100 |100 |
2. Uruchom test Iometer hello inicjowania dysku pamięci podręcznej z następującymi parametrami. Użyj trzech wątków roboczych dla woluminu docelowego hello i głębokości kolejki wynoszącej 128. Ustaw hello hello too2hrs testu na karcie "Testowania instalacji" hello "Czas wykonywania" czas trwania.

   | Scenariusz | Wolumin docelowy | Nazwa | Czas trwania |
   | --- | --- | --- | --- |
   | Inicjowanie dysku pamięci podręcznej |CacheReads |RandomWrites\_1 MB |2hrs |
3. Uruchom test Iometer hello rozgrzewania dysku pamięci podręcznej z następującymi parametrami. Użyj trzech wątków roboczych dla woluminu docelowego hello i głębokości kolejki wynoszącej 128. Ustaw hello hello too2hrs testu na karcie "Testowania instalacji" hello "Czas wykonywania" czas trwania.

   | Scenariusz | Wolumin docelowy | Nazwa | Czas trwania |
   | --- | --- | --- | --- |
   | Ciepłych dysk pamięci podręcznej |CacheReads |RandomReads\_1 MB |2hrs |

Po pamięci podręcznej dysku jest przygotowaniu miejsca, przejdź do scenariuszy testowania hello wymienionych poniżej. Witaj toorun Iometer testu, użyj co najmniej trzech wątków roboczych dla **każdego** woluminu docelowego. Dla każdego wątku roboczego wybierz wolumin docelowy hello, Ustawia głębokość kolejki, a następnie wybierz jedno specyfikacji testu hello zapisane, jak pokazano w tabeli hello poniżej toorun hello odpowiedniego scenariusza testu. Witaj tabeli przedstawiono również oczekiwanych rezultatów IOPS i przepływności podczas uruchamiania tych testów. W przypadku wszystkich scenariuszy mały rozmiar we/wy 8 KB i głębokości kolejki wysoki 128 jest używany.

| Scenariusz testów | Wolumin docelowy | Nazwa | wynik |
| --- | --- | --- | --- |
| Maksymalnie z IOPS odczytu |CacheReads |RandomWrites\_8 kilobajtów |50 000 IOPS |
| Maksymalnie z Zapis IOPS |NoCacheWrites |RandomReads\_8 kilobajtów |IOPS 64 000 |
| Maksymalnie z Łączna liczba IOPS. |CacheReads |RandomWrites\_8 kilobajtów |100 000 IOPS |
| NoCacheWrites |RandomReads\_8 kilobajtów | &nbsp; | &nbsp; |
| Maksymalnie z Odczyt MB/s |CacheReads |RandomWrites\_64 KB |524 MB/s |
| Maksymalnie z Zapisane MB/s |NoCacheWrites |RandomReads\_64 KB |524 MB/s |
| Łączna MB/s |CacheReads |RandomWrites\_64 KB |1000 MB/s |
| NoCacheWrites |RandomReads\_64 KB | &nbsp; | &nbsp; |

Poniżej przedstawiono zrzuty ekranu hello Iometer wyników testu w scalonej scenariuszach IOPS i przepływności.

*Łączna odczyty i zapisy maksymalna liczba IOPS*  
![](media/storage-premium-storage-performance/image9.png)

*Łączna odczyty i zapisy maksymalną przepustowość*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO jest magazynem toobenchmark popularne narzędzia na powitania maszyn wirtualnych systemu Linux. Ma hello elastyczność tooselect różne we/wy rozmiary, sekwencyjnych lub losowych odczyty i zapisy. Go spowoduje utworzenie wątków roboczych lub hello tooperform procesów określony operacji We/Wy. Można określić typu hello operacji We/Wy każdego wątku roboczego należy wykonać przy użyciu plików zadania. Utworzono jeden plik zadania na scenariuszu przedstawiono w poniższych przykładach hello. Możesz zmienić hello specyfikacjach te zadania pliki toobenchmark różnych obciążeń uruchomionych na magazyn w warstwie Premium. W przykładach hello jest używany uruchomiona standardowa maszyna VM 14 DS **Ubuntu**. Użyj hello tę samą konfigurację opisano w hello początku hello [przeprowadzenia testów porównawczych sekcji](#Benchmarking) i ciepłych zapasowej pamięci podręcznej hello przed uruchomieniem hello przeprowadzenia testów porównawczych testów.

Przed rozpoczęciem [Pobierz FIO](https://github.com/axboe/fio) i zainstalować ją na maszynie wirtualnej.

Uruchom następujące polecenie dla Ubuntu, hello

```
apt-get install fio
```

Używamy cztery wątków roboczych dla wspierania operacje zapisu i cztery wątków roboczych dla kierowania operacji odczytu na dyskach hello. Hello pracowników zapisu będzie można kierowania ruchu na wolumin hello "nocache", który ma 10 dysków z pamięci podręcznej ustawić także "None". Hello pracowników odczytu będzie można kierowania ruchu na woluminie hello "readcache", którego za dysk 1 z zestawu w pamięci podręcznej "ReadOnly".

*Zapis maksymalna liczba IOPS*  
Utwórz plik zadania hello z następujących specyfikacji tooget maksymalna liczba IOPS zapisu. Nazwa "fiowrite.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Uwaga hello wykonaj rzeczy, które są zgodne z wytycznymi projektowania hello omówione w poprzednich sekcjach. W tych specyfikacjach są istotne toodrive maksymalna liczba IOPS,  

* Głębokości kolejki wysokiej 256.  
* Mała blok o rozmiarze 8KB.  
* Wiele wątków wykonywania losowe zapisy.

Uruchom hello następujące polecenia tookick poza hello FIO testu przez 30 sekund  

```
sudo fio --runtime 30 fiowrite.ini
```

Podczas wykonywania testu hello będzie możliwe toosee hello liczba zapisu, które są dostarczane hello IOPS dysków maszyny Wirtualnej i Premium. Jak pokazano w poniższym przykładzie hello, hello DS14 maszyny Wirtualnej jest dostarczanie jego zapisu maksymalnego limitu IOPS 50 000 iops.  
    ![](media/storage-premium-storage-performance/image11.png)

*Odczyt maksymalna liczba IOPS*  
Utwórz plik zadania hello z następujących specyfikacji tooget maksymalna liczba IOPS odczytu. Nazwa "fioread.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Uwaga hello wykonaj rzeczy, które są zgodne z wytycznymi projektowania hello omówione w poprzednich sekcjach. W tych specyfikacjach są istotne toodrive maksymalna liczba IOPS,

* Głębokości kolejki wysokiej 256.  
* Mała blok o rozmiarze 8KB.  
* Wiele wątków wykonywania losowe zapisy.

Uruchom hello następujące polecenia tookick poza hello FIO testu przez 30 sekund

```
sudo fio --runtime 30 fioread.ini
```

Podczas wykonywania testu hello będziesz w stanie toosee hello liczba odczytu hello IOPS maszyny Wirtualnej i na tych dysków Premium. Jak pokazano w poniższym przykładzie hello, hello DS14 maszyny Wirtualnej jest dostarczanie więcej niż 64 000 IOPS odczytu. To jest kombinacją hello dysku i hello wydajność pamięci podręcznej.  
    ![](media/storage-premium-storage-performance/image12.png)

*Maksymalna odczytu i zapisu IOPS*  
Utwórz plik zadania hello z następujących specyfikacji tooget maksymalną łączyć odczytu i zapisu IOPS. Nazwa "fioreadwrite.ini".

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Uwaga hello wykonaj rzeczy, które są zgodne z wytycznymi projektowania hello omówione w poprzednich sekcjach. W tych specyfikacjach są istotne toodrive maksymalna liczba IOPS,

* Głębokość kolejki wysoki 128.  
* Mała blok o rozmiarze 4KB.  
* Wiele wątków wykonywania losowe odczytuje i zapisuje.

Uruchom hello następujące polecenia tookick poza hello FIO testu przez 30 sekund

```
sudo fio --runtime 30 fioreadwrite.ini
```

Podczas wykonywania testu hello będzie możliwe toosee hello liczbę połączonych odczytu i zapisu IOPS hello maszyny Wirtualnej i dysków w warstwie Premium są dostarczane. Jak pokazano w poniższym przykładzie hello, hello DS14 maszyny Wirtualnej jest dostarczanie więcej niż 100 000 Scalonej odczytu i zapisu IOPS. To jest kombinacją hello dysku i hello wydajność pamięci podręcznej.  
    ![](media/storage-premium-storage-performance/image13.png)

*Maksymalny łączny przepływności*  
hello tooget maksymalną połączyć odczytu i zapisu przepływności, korzystania z wielu wątków wykonywania odczyty i zapisy większy rozmiar bloku i dużych głębokości. Można użyć blok o rozmiarze 64KB i głębokości kolejki wynoszącej 128.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o usłudze Azure Premium Storage:

* [Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](storage-premium-storage.md)  

Dla użytkowników programu SQL Server zapoznaj się z artykułami na najlepsze rozwiązania w zakresie wydajności programu SQL Server:

* [Wydajność najlepsze rozwiązania dotyczące programu SQL Server na maszynach wirtualnych Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Usługa Azure Premium Storage oferuje najwyższej wydajności programu SQL Server w maszynie Wirtualnej platformy Azure](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
