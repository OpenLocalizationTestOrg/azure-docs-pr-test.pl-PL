---
title: "aaaData replikacji w usłudze Azure Storage | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Replikacja usługi Azure Storage

Witaj danych platformy Microsoft Azure konto magazynu jest zawsze replikowane tooensure trwałości i wysokiej dostępności. Witaj danych, w tym samym centrum danych lub tooa drugi centrum danych, w zależności od opcji replikacji wybierz kopie replikacji. Replikacja chroni dane i zachowuje Twojej aplikacji czasu w przypadku hello przejściowych awarii sprzętu. Jeśli dane są replikowane tooa drugi centrum danych, jest on chroniony z poważnej awarii w lokalizacji głównej hello.

Replikacja zapewnia, że Twoje konto magazynu ma spełnia hello [Umowa dotycząca poziomu usług (SLA) dla magazynu](https://azure.microsoft.com/support/legal/sla/storage/) nawet w fazie hello błędów. Zobacz hello umowy dotyczącej poziomu usług, aby uzyskać informacje na temat usługi Azure Storage zapewnia trwałość i dostępność.

Podczas tworzenia konta magazynu, możesz wybrać następujące opcje replikacji hello:

* [Magazyn lokalnie nadmiarowy (LRS)](#locally-redundant-storage)
* [Magazyn strefowo nadmiarowy (ZRS)](#zone-redundant-storage)
* [Magazyn geograficznie nadmiarowy (GRS)](#geo-redundant-storage)
* [Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)](#read-access-geo-redundant-storage)

Dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS) jest opcja domyślna hello podczas tworzenia konta magazynu.

Witaj w poniższej tabeli zapewnia szybki przegląd hello różnice między LRS, ZRS, GRS i RA-GRS, podczas każdego typu replikacji bardziej szczegółowo adresów w kolejnych sekcjach.

| Strategia replikacji | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Dane są replikowane w wielu centrach danych. |Nie |Tak |Tak |Tak |
| Można odczytać danych z lokalizacji dodatkowej, a także hello lokalizacji głównej. |Nie |Nie |Nie |Tak |
| Liczba kopii danych obsługiwanych w osobnych węzłach. |3 |3 |6 |6 |

Zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/) dla informacji o cenach dla hello nadmiarowość różne opcje.

> [!NOTE]
> Magazyn w warstwie Premium obsługuje magazyn tylko lokalnie nadmiarowy (LRS). Aby uzyskać informacje o magazynie Premium, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Magazyn lokalnie nadmiarowy
Magazyn lokalnie nadmiarowy (LRS) są replikowane trzy razy w ciągu jednostki skalowania magazynu, który znajduje się w centrum danych w regionie hello, w którym utworzono konto magazynu. Żądanie zapisu pomyślnie zwraca tylko wtedy, gdy został zapisany tooall trzy repliki. Te trzy repliki każdego znajdują się w oddzielnych błędów domen i domen uaktualnienia w jeden numer jednostki skalowania.

Jednostki skalowania magazynu to zbiór stojakami węzłów magazynu. Domeny błędów (FD) to grupa węzłów, które reprezentują fizyczną jednostkę awarii i mogą być uważane za należące toohello węzłów tego samego stojak fizycznych. Domeny uaktualnienia (UD) to grupa węzłów, które są ze sobą uaktualniane podczas hello proces uaktualniania usługi (wdrażanie). trzy repliki Hello są rozkładane między UDs i FDs w tooensure jednostki skali jeden magazyn danych jest dostępne, nawet w przypadku awarii sprzętu ma wpływ na jednym stojaku lub po uaktualnieniu węzłów podczas wdrażania.

Magazyn LRS jest hello najniższy koszt opcji i udostępnia opcje tooother usługi co najmniej trwałości w porównaniu. W przypadku awarii poziomu Centrum danych (fire zalewania itp.) hello wszystkie trzy repliki może być utracone lub ich nieodwracalnej utraty. toomitigate to ryzyko, z magazynu geograficznie nadmiarowego magazynu (GRS) jest zalecane dla większości aplikacji.

Magazyn lokalnie nadmiarowy nadal może być wskazane w niektórych scenariuszach:

* Zapewnia najwyższy maksymalna przepustowość opcji replikacji magazynu Azure.
* Jeśli aplikacja przechowuje dane, które można łatwo odtworzyć, można wybrać opcję LRS.
* Niektóre aplikacje są ograniczone tooreplicating dane tylko w obrębie kraju powodu toodata wymagania ładu. Region sparowanego może być w innym kraju. Aby uzyskać więcej informacji na pary regionu, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Magazyn strefowo nadmiarowy
Magazyn strefowo nadmiarowy (ZRS) asynchronicznie replikuje dane między centrami danych w ramach jednego lub dwóch regionach dodanie toostoring trzy repliki podobne tooLRS, zapewniając większą trwałość niż magazyn LRS. Dane przechowywane w ZRS jest trwały, nawet jeśli hello podstawowego centrum danych jest niedostępne lub ich nieodwracalnej utraty.
Klienci, którzy planują toouse ZRS należy pamiętać, że:

* Magazyn ZRS jest dostępna tylko dla blokowych obiektów blob na kontach magazynu ogólnego przeznaczenia i jest obsługiwana tylko w wersjach usługi magazynu 2014-02-14 lub nowszej.
* Ponieważ asynchroniczną replikację wiąże się z opóźnieniem, w przypadku hello lokalnego po awarii, który jest to możliwe, że zmiany, które nie zostały jeszcze zreplikowane toohello dodatkowej zostaną utracone, jeśli hello danych nie można odzyskać z hello podstawowego.
* Witaj repliki nie mogą być dostępne aż do trybu failover toohello dodatkowej inicjuje firmy Microsoft.
* Nie można przekonwertować kontami ZRS, nowsze tooLRS lub GRS. Podobnie, istniejące konto LRS lub GRS nie może być przekonwertowany tooa ZRS konta.
* Nie masz kontami ZRS, metryki lub możliwości rejestrowania.

## <a name="geo-redundant-storage"></a>Magazyn geograficznie nadmiarowy
Magazyn geograficznie nadmiarowy (GRS) replikuje regionu dodatkowej tooa danych będącego setki odległości od regionu podstawowego hello. Jeśli konto magazynu ma GRS włączone, dane są trwałe nawet w przypadku hello pełną regionalnej awarii lub awarii, w których hello regionu podstawowego nie jest możliwe do odzyskania.

Dla konta magazynu z GRS włączone aktualizacja jest pierwszym regionu podstawowego toohello zatwierdzone, w których są replikowane trzy razy. Następnie aktualizacji hello są replikowane asynchronicznie toohello region pomocniczy, w których również są replikowane trzy razy.

W wypadku magazynu GRS obu regionów podstawowych i pomocniczych hello zarządzania replik w domenach awarii oddzielne i uaktualnienia domen w obrębie jednostki skalowania magazynu zgodnie z opisem z LRS.

Kwestie do rozważenia:

* Ponieważ asynchroniczną replikację wiąże się z opóźnieniem, w przypadku regionalnej awarii jest możliwe, że zmiany, które nie zostały jeszcze zreplikowane hello region pomocniczy toohello zostaną utracone, jeśli nie można odzyskać danych powitania od regionu podstawowego hello.
* Replika Hello jest niedostępna, chyba że Microsoft inicjuje region pomocniczy toohello trybu failover. Jeśli Microsoft inicjuje region pomocniczy toohello trybu failover, konieczne będzie odczytu i zapisu danych toothat po zakończeniu pracy awaryjnej hello. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące odzyskiwania po awarii](../storage-disaster-recovery-guidance.md). 
* Jeśli aplikacja potrzebuje tooread z regionu pomocniczego hello, użytkownik hello włączyć RA-GRS.

Podczas tworzenia konta magazynu, należy wybrać hello regionie podstawowym konta hello. region pomocniczy Hello jest określany na podstawie hello regionu podstawowego i nie można zmienić. Witaj w poniższej tabeli przedstawiono par podstawowych i pomocniczych region hello.

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
> Region pomocniczy Virginia wersji dla instytucji rządowych USA jest Texas nam wersji dla instytucji rządowych. Wcześniej Virginia nam wersji dla instytucji rządowych wykorzystana Iowa nam wersji dla instytucji rządowych jako regionie pomocniczym. Konta magazynu z równoczesnym wykorzystaniem Iowa nam wersji dla instytucji rządowych, zgodnie z regionu pomocniczego są migrowane tooUS Texas wersji dla instytucji rządowych jako region pomocniczej. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Dostęp do odczytu magazynu geograficznie nadmiarowego
Dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS) pozwala zwiększyć dostępność dla konta magazynu, dostarczając danych toohello dostęp tylko do odczytu w lokalizacji dodatkowej hello, oprócz replikacji toohello dwóch regionach podał grs w warstwie.

Po włączeniu dostępu tylko do odczytu danych tooyour w regionie pomocniczym hello danych jest dostępna na dodatkowej punktu końcowego, w dodanie toohello podstawowy punkt końcowy dla konta magazynu. pomocniczy punkt końcowy Hello jest podobne podstawowy punkt końcowy toohello, ale dołącza sufiks hello `–secondary` toohello nazwy konta. Na przykład, jeśli podstawowy dla punktu końcowego hello usługi obiektów Blob jest `myaccount.blob.core.windows.net`, to jest punkt końcowy dodatkowej `myaccount-secondary.blob.core.windows.net`. Witaj klucze dostępu dla konta magazynu są hello tego samego dla obu hello głównych i dodatkowych punktów końcowych.

Kwestie do rozważenia:

* Aplikacja ma toomanage którym punktem końcowym, używając RA-GRS prowadzi interakcję z.
* Ponieważ asynchroniczną replikację wiąże się z opóźnieniem, w przypadku regionalnej awarii jest możliwe, że zmiany, które nie zostały jeszcze zreplikowane hello region pomocniczy toohello zostaną utracone, jeśli nie można odzyskać danych powitania od regionu podstawowego hello.
* Jeśli Microsoft inicjuje region pomocniczy toohello trybu failover, konieczne będzie odczytu i zapisu danych toothat po zakończeniu pracy awaryjnej hello. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące odzyskiwania po awarii](../storage-disaster-recovery-guidance.md). 
* RA-GRS jest przeznaczony dla celów wysokiej dostępności. Wskazówki dotyczące skalowalności, przejrzyj hello [Lista kontrolna wydajności](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Często zadawane pytania

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Jak zmienić typ replikacji geograficznie hello mojego konta magazynu?

   Hello geograficznie replikacji typ konta magazynu między LRS, GRS, można zmienić i RA-GRS przy użyciu hello [portalu Azure](https://portal.azure.com/), [programu Azure Powershell](storage-powershell-guide-full.md) lub programowo przy użyciu jednej z naszych wiele klienta magazynu Biblioteki. Należy pamiętać, że kontami ZRS nie może być przekonwertowany LRS lub GRS. Podobnie, istniejące konto LRS lub GRS nie może być przekonwertowany tooa ZRS konta.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Będzie żadnego czas przestoju zmiana hello typ replikacji konta magazynu?

   Nie, nie będzie żadnego czas przestoju.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Będzie żadnych dodatkowych kosztów zmiana hello typ replikacji konta magazynu?

   Tak. W przypadku zmiany z tooGRS LRS (lub RA-GRS) dla konta magazynu, może zostać obciążony dodatkowe opłaty za wyjście objętego kopiowanie istniejących danych z lokalizacji dodatkowej toohello lokalizacji głównej. Po hello początkowe dane są kopiowane nie ma już wyjście dodatkowe opłaty za replikowanie danych hello z hello toosecondary głównej lokalizacji geo. Szczegóły Hello opłat przepustowości można znaleźć na powitania [cennik usługi Azure Storage strony](https://azure.microsoft.com/pricing/details/storage/blobs/). W przypadku zmiany z GRS tooLRS, nie ma żadnych dodatkowych kosztów, ale dane zostaną usunięte z lokalizacji dodatkowej hello.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Jak RA-GRS może mi pomóc?
   
   Magazyn GRS zapewnia replikację danych z regionu pomocniczego tooa podstawowego, który jest setki odległości od regionu podstawowego hello. W takim przypadku dane są trwałe nawet w przypadku hello pełną regionalnej awarii lub awarii, w których hello regionu podstawowego nie jest możliwe do odzyskania. RA-GRS magazynu zawiera tę plus dodaje hello możliwości tooread hello danych z lokalizacji dodatkowej hello. W przypadku sugestii dotyczących tooleverage tę możliwość, można znaleźć za[Projektowanie wysoce dostępnych aplikacji przy użyciu magazynu RA-GRS](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Czy istnieje sposób dla mnie toofigure limit czasu wykonywania tooreplicate dane z regionu pomocniczego hello toohello podstawowego?
   
   Jeśli używasz magazynu RA-GRS, można sprawdzić hello czas ostatniej synchronizacji z konta magazynu. Czas ostatniej synchronizacji jest wartość daty/godziny GMT; wszystkie zapisy głównej przed hello czas ostatniej synchronizacji został pomyślnie napisany toohello lokalizacji dodatkowej, co oznacza, że są one dostępne toobe odczytu z lokalizacji dodatkowej hello. Podstawowy zapisuje po hello czas ostatniej synchronizacji może lub mogą nie być dostępne dla odczytów jeszcze. Można zbadać tę wartość przy użyciu hello [portalu Azure](https://portal.azure.com/), [programu Azure PowerShell](storage-powershell-guide-full.md), lub programowo przy użyciu hello interfejsu API REST lub jeden z hello biblioteki klienta magazynu. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Jak można zmienić regionu pomocniczego toohello w przypadku wystąpienia awarii w regionie podstawowym hello?
   
   Można znaleźć w artykule toohello [jakie toodo w przypadku wystąpienia awarii usługi Azure Storage](../storage-disaster-recovery-guidance.md) więcej szczegółów.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. Co to jest hello RPO i RTO z GRS?
   
   Cel punktu odzyskiwania (RPO): W GRS i RA-GRS hello magazynu usługi asynchronicznie są replikowane geograficznie hello danych z lokalizacji dodatkowej hello toohello podstawowego. Jeśli jest poważnej awarii regionalnych i trybu failover ma wykonać toobe, ostatnie zmiany różnicowe, które nie zostały jeszcze replikacją geograficzną mogą zostać utracone. Hello liczba minut potencjalnych utraconych danych jest hello tooas określonego RPO (co oznacza, że mogą zostać odzyskane hello punktu w czasie toowhich danych). Zwykle mamy RPO mniej niż 15 minut, chociaż jest obecnie przyjmuje umowy dotyczącej poziomu usług na jak długo replikacja geograficzna.

   Celu czasu odzyskiwania (RTO): Jest to miara, jak długo trwa trybu failover hello toodo i odzyskać konto magazynu hello online jeśli mamy toodo trybu failover. Hello czasu toodo hello w tryb failover zawiera następujące hello:
    * czas Hello trwa tooinvestigate i określić, jeśli firma Microsoft może odzyskać dane hello w lokalizacji głównej hello lub potrzebujemy toodo trybu failover.
    * Konto hello trybu failover, zmieniając hello DNS wpisy toopoint toohello dodatkowej lokalizacji głównej.

   Firma ponosi odpowiedzialności hello bardzo poważnie zachowania danych, dzięki czemu w przypadku wystąpienia odzyskiwanie danych hello, firma Microsoft będzie blokadę na wykonanie pracy awaryjnej hello i skupić się na odzyskiwanie danych hello w lokalizacji głównej hello. W przyszłości hello, planujemy tooallow tooprovide interfejsu API można tootrigger przejściu w tryb failover na poziomie konta, które następnie pozwoli toocontrol hello RTO samodzielnie, ale to nie jest jeszcze dostępna.
   
## <a name="next-steps"></a>Następne kroki
* [Projektowanie aplikacji wysokiej dostępności przy użyciu magazynu RA-GRS](../storage-designing-ha-apps-with-ragrs.md)
* [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Informacji o kontach magazynu Azure](../storage-create-storage-account.md)
* [Azure cele wydajności i skalowalności magazynu](storage-scalability-targets.md)
* [Microsoft Azure Storage nadmiarowość opcje i dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP Paper - Azure Storage: Wysoce dostępna usługa magazynu w chmurze z wysoki poziom spójności](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

