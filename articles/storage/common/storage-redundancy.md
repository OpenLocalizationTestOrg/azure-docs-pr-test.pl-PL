---
title: "Replikacja danych w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dane na koncie usługi Magazyn Microsoft Azure jest replikowana na potrzeby trwałości i wysokiej dostępności. Opcje replikacji obejmują magazyn lokalnie nadmiarowy (LRS), Magazyn strefowo nadmiarowy (ZRS) magazynu geograficznie nadmiarowego (GRS) i dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS)."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: c35f53c5c80a67cb33b457e9e3235d0e745536cf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-replication"></a>Replikacja usługi Azure Storage

Dane konta usługi Microsoft Azure Storage są zawsze replikowane w celu zapewnienia trwałości i wysokiej dostępności. W zależności od wybranej opcji replikacji dane są kopiowane w ramach tego samego centrum danych lub do innego centrum danych. Replikacja chroni dane i utrzymuje sprawne działanie aplikacji w wypadku przejściowych awarii sprzętu. Jeśli dane są replikowane do drugiego centrum danych, jest on chroniony z poważnej awarii w lokalizacji głównej.

Replikacja gwarantuje, że Twoje konto magazynu spełnia warunki [Umowy dotyczącej poziomu usług (SLA) dla Magazynu](https://azure.microsoft.com/support/legal/sla/storage/) nawet w przypadku wystąpienia błędów. Zobacz umowę SLA, aby uzyskać informacje o gwarancjach usługi Azure Storage dotyczących trwałości i dostępności.

Podczas tworzenia konta magazynu można wybrać jedną z następujących opcji replikacji:

* [Magazyn lokalnie nadmiarowy (LRS)](#locally-redundant-storage)
* [Magazyn strefowo nadmiarowy (ZRS)](#zone-redundant-storage)
* [Magazyn geograficznie nadmiarowy (GRS)](#geo-redundant-storage)
* [Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)](#read-access-geo-redundant-storage)

Dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS) jest domyślną opcją podczas tworzenia konta magazynu.

Poniższa tabela zawiera szybki przegląd różnice między LRS, ZRS, GRS i RA-GRS, podczas każdego typu replikacji bardziej szczegółowo adresów w kolejnych sekcjach.

| Strategia replikacji | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Dane są replikowane w wielu centrach danych. |Nie |Tak |Tak |Tak |
| Można odczytać danych z lokalizacji dodatkowej, a także lokalizacji głównej. |Nie |Nie |Nie |Tak |
| Liczba kopii danych obsługiwanych w osobnych węzłach. |3 |3 |6 |6 |

Zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/) dla informacji o cenach dla opcji różnych nadmiarowości.

> [!NOTE]
> Magazyn w warstwie Premium obsługuje magazyn tylko lokalnie nadmiarowy (LRS). Aby uzyskać informacje o magazynie Premium, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Magazyn lokalnie nadmiarowy
Magazyn lokalnie nadmiarowy (LRS) są replikowane trzy razy w ciągu jednostki skalowania magazynu, który znajduje się w centrum danych w regionie, w którym utworzono konto magazynu. Żądanie zapisu pomyślnie zwraca tylko wtedy, gdy został zapisany do wszystkie trzech repliki. Te trzy repliki każdego znajdują się w oddzielnych błędów domen i domen uaktualnienia w jeden numer jednostki skalowania.

Jednostki skalowania magazynu to zbiór stojakami węzłów magazynu. Domeny błędów (FD) to grupa węzłów, które reprezentują fizyczną jednostkę awarii i mogą być uważane za węzłach należących do tej samej fizycznej stojaku. Domeny uaktualnienia (UD) to grupa węzłów, które są ze sobą uaktualniony podczas procesu uaktualniania usługi (wdrażanie). Trzy repliki są rozkładane między UDs i FDs w jedną jednostkę skalowania magazynu, aby upewnić się, czy dane są dostępne, nawet w przypadku awarii sprzętu ma wpływ na jednym stojaku lub po uaktualnieniu węzłów podczas wdrażania.

Magazyn LRS jest opcją najniższy koszt i oferuje co najmniej trwałości w porównaniu do innych opcji. W przypadku awarii poziomu Centrum danych (fire zalewania itp.) wszystkie trzy repliki może być utracone lub ich nieodwracalnej utraty. Aby zmniejszyć to zagrożenie, z magazynu geograficznie nadmiarowego magazynu (GRS) jest zalecane dla większości aplikacji.

Magazyn lokalnie nadmiarowy nadal może być wskazane w niektórych scenariuszach:

* Zapewnia najwyższy maksymalna przepustowość opcji replikacji magazynu Azure.
* Jeśli aplikacja przechowuje dane, które można łatwo odtworzyć, można wybrać opcję LRS.
* Niektóre aplikacje są ograniczone do replikowanie danych tylko w obrębie kraju ze względu na wymagania ładu danych. Region sparowanego może być w innym kraju. Aby uzyskać więcej informacji na pary regionu, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Magazyn strefowo nadmiarowy
Magazyn strefowo nadmiarowy (ZRS) asynchronicznie replikuje dane między centrami danych w ramach jednego lub dwóch regionach oprócz przechowywania trzy repliki, podobnie jak LRS, zapewniając większą trwałość niż magazyn LRS. Dane przechowywane w ZRS jest trwały, nawet jeśli podstawowe centrum danych jest niedostępny lub ich nieodwracalnej utraty.
Klienci planujący używaj technologii ZRS, należy pamiętać, że:

* Magazyn ZRS jest dostępna tylko dla blokowych obiektów blob na kontach magazynu ogólnego przeznaczenia i jest obsługiwana tylko w wersjach usługi magazynu 2014-02-14 lub nowszej.
* Ponieważ asynchroniczną replikację obejmuje opóźnienia, w przypadku lokalnego po awarii jest możliwe, że zmiany, które nie zostały jeszcze zreplikowane na serwerze pomocniczym zostaną utracone, jeśli nie można odzyskać dane z serwera podstawowego.
* Replika nie mogą być dostępne, dopóki nie pomocniczym w tryb failover inicjuje firmy Microsoft.
* Kontami ZRS nie można przekonwertować później LRS lub GRS. Podobnie istniejące konto LRS lub GRS nie można przekonwertować na konto ZRS.
* Nie masz kontami ZRS, metryki lub możliwości rejestrowania.

## <a name="geo-redundant-storage"></a>Magazyn geograficznie nadmiarowy
Magazyn geograficznie nadmiarowy (GRS) replikuje dane w regionie pomocniczym będący setki odległości od regionu podstawowego. Jeśli konto magazynu ma GRS włączone, dane są trwałe nawet w przypadku pełnej regionalnej awarii lub awarii, w którym regionie podstawowym nie jest możliwe do odzyskania.

Dla konta magazynu z GRS włączone aktualizacja najpierw przywiązuje dużą wagę do regionu podstawowego, w których są replikowane trzy razy. Aktualizacja jest następnie replikowane asynchronicznie w regionie pomocniczym, których również są replikowane trzy razy.

W wypadku magazynu GRS podstawowych i pomocniczych regionów zarządzania replik w domenach awarii oddzielne i uaktualnienia domen w obrębie jednostki skalowania magazynu zgodnie z opisem z LRS.

Kwestie do rozważenia:

* Ponieważ asynchroniczną replikację obejmuje opóźnienia, w przypadku regionalnej awarii jest możliwe, że zmiany, które nie zostały jeszcze zreplikowane w regionie pomocniczym zostaną utracone, jeśli nie można odzyskać dane z regionu podstawowego.
* Replika nie jest dostępna, chyba że Microsoft inicjuje trybu failover w regionie pomocniczym. Jeśli Microsoft Zainicjuj tryb failover w regionie pomocniczym, będą mieć odczytu i zapisu do tych danych po przejściu w tryb failover została ukończona. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące odzyskiwania po awarii](../storage-disaster-recovery-guidance.md). 
* Jeśli aplikacja będzie można odczytać z regionu pomocniczego, użytkownik powinien włączyć RA-GRS.

Po utworzeniu konta magazynu, należy wybrać regionie podstawowym konta. Region pomocniczy jest określany na podstawie regionu podstawowego i nie można zmienić. W poniższej tabeli przedstawiono par regionu podstawowego i pomocniczego.

| Podstawowy | Pomocniczy |
| --- | --- |
| Środkowo-północne stany USA |Środkowo-południowe stany USA |
| Środkowo-południowe stany USA |Środkowo-północne stany USA |
| Wschodnie stany USA |Zachodnie stany USA |
| Zachodnie stany USA |Wschodnie stany USA |
| Wschodnie stany USA 2 |Środkowe stany USA |
| Środkowe stany USA |Wschodnie stany USA 2 |
| Europa Północna |Europa Zachodnia |
| Europa Zachodnia |Europa Północna |
| Azja Południowo-Wschodnia |Azja Wschodnia |
| Azja Wschodnia |Azja Południowo-Wschodnia |
| Chiny Wschodnie |Chiny Północne |
| Chiny Północne |Chiny Wschodnie |
| Japonia Wschodnia |Japonia Zachodnia |
| Japonia Zachodnia |Japonia Wschodnia |
| Brazylia Południowa |Środkowo-południowe stany USA |
| Australia Wschodnia |Australia Południowo-Wschodnia |
| Australia Południowo-Wschodnia |Australia Wschodnia |
| Indie Południowe |Indie Środkowe |
| Indie Środkowe |Indie Południowe |
| Indie Zachodnie |Indie Południowe |
| Administracja USA — Iowa |Administracja USA — Wirginia |
| Administracja USA — Wirginia |Administracja USA — Teksas |
| Administracja USA — Teksas |Administracja USA — Arizona |
| Administracja USA — Arizona |Administracja USA — Teksas |
| Kanada Środkowa |Kanada Wschodnia |
| Kanada Wschodnia |Kanada Środkowa |
| Zachodnie Zjednoczone Królestwo |Południowe Zjednoczone Królestwo |
| Południowe Zjednoczone Królestwo |Zachodnie Zjednoczone Królestwo |
| Niemcy Środkowe |Niemcy Północno-Wschodnie |
| Niemcy Północno-Wschodnie |Niemcy Środkowe |
| Zachodnie stany USA 2 |Środkowo-zachodnie stany USA |
| Środkowo-zachodnie stany USA |Zachodnie stany USA 2 |

Aby uzyskać aktualne informacje o obsługiwane przez platformę Azure, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

>[!NOTE]  
> Region pomocniczy Virginia wersji dla instytucji rządowych USA jest Texas nam wersji dla instytucji rządowych. Wcześniej Virginia nam wersji dla instytucji rządowych wykorzystana Iowa nam wersji dla instytucji rządowych jako regionie pomocniczym. Równoczesnym wykorzystaniem Iowa nam wersji dla instytucji rządowych jako regionu pomocniczego konta magazynu są migrowane do nas wersji dla instytucji rządowych Texas jako region pomocniczej. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Dostęp do odczytu magazynu geograficznie nadmiarowego
Dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS) maksymalizację dostępności dla konta magazynu, zapewniając dostęp tylko do odczytu do danych w dodatkowej lokalizacji, oprócz replikacji dwóch regionach podał grs w warstwie.

Po włączeniu dostępu tylko do odczytu do danych w regionie pomocniczym, Twoje dane są dostępne na pomocniczy punkt końcowy, oprócz podstawowego punktu końcowego dla konta magazynu. Pomocniczy punkt końcowy jest podobny do podstawowego punktu końcowego, ale dołącza sufiks `–secondary` do nazwy konta. Na przykład, jeśli jest podstawowym punktu końcowego usługi Blob `myaccount.blob.core.windows.net`, to jest punkt końcowy dodatkowej `myaccount-secondary.blob.core.windows.net`. Klawisze dostępu dla konta magazynu są takie same dla obu głównych i dodatkowych punktów końcowych.

Kwestie do rozważenia:

* Aplikacja musi zarządzać którym punktem końcowym, używając RA-GRS prowadzi interakcję z.
* Ponieważ asynchroniczną replikację obejmuje opóźnienia, w przypadku regionalnej awarii jest możliwe, że zmiany, które nie zostały jeszcze zreplikowane w regionie pomocniczym zostaną utracone, jeśli nie można odzyskać dane z regionu podstawowego.
* Jeśli Microsoft inicjuje trybu failover w regionie pomocniczym, będą mieć odczytu i zapisu do tych danych po przejściu w tryb failover została ukończona. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące odzyskiwania po awarii](../storage-disaster-recovery-guidance.md). 
* RA-GRS jest przeznaczony dla celów wysokiej dostępności. Wskazówki dotyczące skalowalności, przejrzyj [Lista kontrolna wydajności](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Często zadawane pytania

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-the-geo-replication-type-of-my-storage-account"></a>1. Jak zmienić typ replikacji geograficznie moim koncie magazynu?

   Typ replikacji geograficznie między LRS, GRS i RA-GRS przy użyciu konta magazynu można zmienić [portalu Azure](https://portal.azure.com/), [programu Azure Powershell](storage-powershell-guide-full.md) lub programowo przy użyciu jednej z naszych wiele bibliotek klienckich magazynu . Należy pamiętać, że kontami ZRS nie może być przekonwertowany LRS lub GRS. Podobnie istniejące konto LRS lub GRS nie można przekonwertować na konto ZRS.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-the-replication-type-of-my-storage-account"></a>2. Będzie żadnego czas przestoju zmiana typ replikacji konta magazynu?

   Nie, nie będzie żadnego czas przestoju.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-the-replication-type-of-my-storage-account"></a>3. Będzie żadnych dodatkowych kosztów zmiana typ replikacji konta magazynu?

   Tak. W przypadku zmiany z replikacji LRS na GRS (lub RA-GRS) dla konta magazynu, może zostać obciążony dodatkowe opłaty za wyjście objętego kopiowanie istniejących danych z lokalizacji podstawowej do dodatkowej lokalizacji. Po początkowej dane są kopiowane jest bezpłatna dalsze dodatkowe wyjście dla replikowanych danych z serwera podstawowego do lokalizacji dodatkowej geograficzna. Szczegóły dotyczące opłat przepustowości można znaleźć w [cennik usługi Azure Storage strony](https://azure.microsoft.com/pricing/details/storage/blobs/). Jeśli zmienisz z GRS LRS, nie ma żadnych dodatkowych kosztów, ale dane zostaną usunięte z lokalizacji dodatkowej.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Jak RA-GRS może mi pomóc?
   
   Magazyn GRS zapewnia replikację danych z głównego w regionie pomocniczym będący setki odległości od regionu podstawowego. W takim przypadku dane są trwałe nawet w przypadku pełnej regionalnej awarii lub awarii, w którym regionie podstawowym nie jest możliwe do odzyskania. RA-GRS magazynu zawiera tę plus dodaje możliwości odczytu danych z lokacji dodatkowej. Sugestii o tym, jak wykorzystać tę możliwość, można znaleźć na stronie [Projektowanie wysoce dostępnych aplikacji przy użyciu magazynu RA-GRS](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-to-figure-out-how-long-it-takes-to-replicate-my-data-from-the-primary-to-the-secondary-region"></a>5. Czy istnieje sposób dowiedzieć się, jak długo trwa replikowanie danych z serwera podstawowego w regionie pomocniczym?
   
   Jeśli używasz magazynu RA-GRS, można sprawdzić czas ostatniej synchronizacji z konta magazynu. Czas ostatniej synchronizacji jest wartość daty/godziny GMT; wszystkie zapisy głównej przed czas ostatniej synchronizacji zostały pomyślnie zapisane w lokalizacji dodatkowej, średniej, które są dostępne do odczytu z lokalizacji dodatkowej. Podstawowy zapisuje po czas ostatniej synchronizacji może lub mogą nie być dostępne dla odczytów jeszcze. Można badać przy użyciu tej wartości [portalu Azure](https://portal.azure.com/), [programu Azure PowerShell](storage-powershell-guide-full.md), lub programowo przy użyciu interfejsu API REST lub jednej z bibliotek klienckich magazynu. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-to-the-secondary-region-if-there-is-an-outage-in-the-primary-region"></a>6. Jak można przełączyć w regionie pomocniczym w przypadku wystąpienia awarii w regionie podstawowym?
   
   Można znaleźć w artykule [co robić w przypadku wystąpienia awarii usługi Azure Storage](../storage-disaster-recovery-guidance.md) więcej szczegółów.

<a id="rpo-rto"></a>
#### <a name="7-what-is-the-rpo-and-rto-with-grs"></a>7. Co to jest RPO i RTO z GRS?
   
   Cel punktu odzyskiwania (RPO): W GRS i RA-GRS, magazyn usługi asynchronicznie geograficznie są replikowane dane z serwera podstawowego do lokalizacji dodatkowej. Jeśli jest poważnej awarii regionalnych i trybu failover ma zostać wykonana, ostatnie zmiany różnicowe, które nie zostały jeszcze replikacją geograficzną mogą zostać utracone. Liczbę minut potencjalnych utraconych danych jest określone jako cel punktu odzyskiwania (co oznacza, że punkt w czasie, do którego można odzyskać dane). Zwykle mamy RPO mniej niż 15 minut, chociaż jest obecnie przyjmuje umowy dotyczącej poziomu usług na jak długo replikacja geograficzna.

   Celu czasu odzyskiwania (RTO): Jest to miara czasu wykonywania nam w tryb failover i Pobierz konta magazynu do trybu online, jeśli mamy tryb failover. Czas na wykonanie pracy awaryjnej obejmuje następujące funkcje:
    * Czas potrzebny nam zbadać i określić, czy firma Microsoft może odzyskać dane w lokalizacji głównej czy musimy tryb failover.
    * Tryb failover konta, zmieniając głównej wpisy DNS wskaż lokalizację dodatkowej.

   Firma Microsoft odpowiedzialni bardzo poważnie zachowania danych, dzięki czemu w przypadku jakakolwiek możliwość odzyskania danych, firma Microsoft będzie blokadę na wykonanie pracy awaryjnej i skupić się na odzyskiwanie danych w lokalizacji głównej. W przyszłości firma Microsoft planuje dostarczać interfejs API umożliwia wyzwolić tryb failover na poziomie konta, który następnie umożliwi kontrolować RTO samodzielnie, ale to nie jest jeszcze dostępna.
   
## <a name="next-steps"></a>Następne kroki
* [Projektowanie aplikacji wysokiej dostępności przy użyciu magazynu RA-GRS](../storage-designing-ha-apps-with-ragrs.md)
* [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Informacji o kontach magazynu Azure](../storage-create-storage-account.md)
* [Azure cele wydajności i skalowalności magazynu](storage-scalability-targets.md)
* [Microsoft Azure Storage nadmiarowość opcje i dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP Paper - Azure Storage: Wysoce dostępna usługa magazynu w chmurze z wysoki poziom spójności](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

