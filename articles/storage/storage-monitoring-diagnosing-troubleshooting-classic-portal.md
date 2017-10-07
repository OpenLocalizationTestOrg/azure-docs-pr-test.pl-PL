---
title: "aaaMonitor, diagnozowanie i rozwiązywanie problemów z magazynu | Dokumentacja firmy Microsoft"
description: "Korzystać z funkcji, takich jak analizy magazynu, rejestrowania po stronie klienta i innych tooidentify narzędzi innych firm, diagnozowanie i rozwiązywanie problemów związanych z usługą Azure Storage."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: da57e844-705d-449d-8ed5-5607d2a6170b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: fhryo-msft
ms.openlocfilehash: 294a0bd27bd03913e01a719c0175cab827d58225
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Monitorowanie, diagnozowanie i rozwiązywanie problemów z usługą Microsoft Azure Storage
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Omówienie
Może być bardziej skomplikowane niż w tradycyjnych środowisk diagnozowania i rozwiązywania problemów w aplikacji rozproszonej hostowanych w środowisku chmury. Aplikacje można wdrażać w infrastrukturze PaaS lub IaaS lokalnie na urządzeniu przenośnym lub w kombinacji tych. Zazwyczaj ruchu sieciowego aplikacji może przechodzić między nimi sieci publicznych i prywatnych aplikacja może korzystać z wielu technologii magazynowania, takich jak Microsoft Azure magazynu tabel, obiektów blob, kolejek i przechowuje pliki danych tooother dodanie, takie jak relacyjna i baz danych dokumentu.

toomanage takich aplikacji pomyślnie należy monitorować je z wyprzedzeniem i zrozumieć, jak toodiagnose i rozwiązywać problemy dotyczące wszystkich aspektów je i ich technologie zależne. Jako użytkownik usługi Azure Storage, należy stale monitorowania usług magazynu hello aplikacja używa nieoczekiwane zmiany w zachowaniu (na przykład wolniej niż zwykle reakcje) i użyć rejestrowania toocollect bardziej szczegółowe dane i tooanalyze Wystąpił problem w głębokość. informacje diagnostyczne Hello, który można uzyskać od monitorowanie i rejestrowanie pomoże możesz toodetermine hello głównej przyczyny hello wystawiać Aplikacja napotkała. Następnie można rozwiązać problem hello i określić hello odpowiednie czynności, które można wykonać tooremediate go. Usługa Azure Storage jest podstawowa usługi Azure i stanowi ważną część hello większość rozwiązań klientów do wdrożenia toohello infrastruktury platformy Azure. Magazyn Azure obejmuje możliwości toosimplify monitorowanie, diagnozowanie i rozwiązywanie problemów z magazynowaniem w aplikacjach opartych na chmurze.

> [!NOTE]
> Konta magazynu typu replikacji z magazynu Strefowo nadmiarowy (ZRS) nie mają metryki hello lub funkcja rejestrowania teraz włączone. 
> 
> 

Dla przewodnika praktyczne tooend-to-end rozwiązywania problemów w aplikacji usługi Azure Storage, zobacz [Rozwiązywanie problemów przy użyciu metryk usługi Azure Storage i rejestrowania, AzCopy i Message Analyzer End-to-End](storage-e2e-troubleshooting.md).

* [Wprowadzenie]
  * [Jak jest zorganizowana w tym przewodniku]
* [monitorowania usługi magazynu]
  * [Monitorowanie kondycji usługi]
  * [Monitorowanie wydajności]
  * [Monitorowanie dostępności]
  * [Monitorowanie wydajności]
* [diagnozowanie problemów z magazynowaniem]
  * [Problemy z usługi kondycji]
  * [Problemy z wydajnością]
  * [Diagnozowanie błędów]
  * [Problemy z emulatora magazynu]
  * [Narzędzia rejestrowania magazynu]
  * [Przy użyciu narzędzia rejestracji w sieci]
* [śledzenia End-to-end]
  * [Korelowanie dane dziennika]
  * [Identyfikator żądania klienta]
  * [identyfikator żądania serwera]
  * [Znaczniki czasu]
* [wskazówki rozwiązywania problemów]
  * [metryki pokazują AverageE2ELatency wysoki i niski AverageServerLatency]
  * [Metryki pokazują AverageE2ELatency niski i niski AverageServerLatency, ale występuje duże opóźnienie powitania klienta]
  * [Metryki wskazują wysoką wartość AverageServerLatency]
  * [Występują nieoczekiwane opóźnienia w dostarczaniu komunikatów w kolejce]
  * [metryki spowodować wzrost PercentThrottlingError]
  * [metryki spowodować wzrost PercentTimeoutError]
  * [Metryki wskazują wzrost wartości PercentNetworkError]
  * [powitania klienta odbiera komunikaty HTTP 403 (Dostęp zabroniony)]
  * [powitania klienta odbiera komunikaty HTTP 404 (nie znaleziono)]
  * [powitania klienta odbiera komunikaty HTTP 409 (konflikt)]
  * [metryki pokazują PercentSuccess niskim lub wpisy dziennika analizy zawierać operacje z Stan transakcji ClientOtherErrors]
  * [Metryki pojemności Pokaż nieoczekiwane zwiększenie wykorzystania pojemności magazynu]
  * [Występują nieoczekiwane ponowne uruchomienie maszyn wirtualnych, które mają wiele wirtualnych dysków twardych dołączonych]
  * [Problem wynika z przy użyciu emulatora magazynu hello do rozwoju lub testu]
  * [Pojawiły się problemy z instalacją hello Azure SDK dla platformy .NET]
  * [Inny problem z usługą magazynu]
* [dodatki]
  * [dodatku 1: ruchu HTTP i HTTPS toocapture przy użyciu narzędzia Fiddler]
  * [dodatek 2: ruchu sieciowego przy użyciu programu Wireshark toocapture]
  * [dodatku 3: ruchu sieciowego przy użyciu programu Microsoft Message Analyzer toocapture]
  * [Dodatek 4: Przy użyciu danych metryki i dziennika tooview programu Excel]
  * [dodatek 5: monitorowanie za pomocą usługi Application Insights dla programu Visual Studio Team Services]

## <a name="introduction"></a>Wprowadzenie
Problemy związane z ten przewodnik przedstawia należy jak toouse funkcji takich jak analiza magazynu Azure, rejestrowania po stronie klienta w hello biblioteki klienta magazynu Azure i innych tooidentify narzędzi innych firm, diagnozowania i rozwiązywania problemów usługi Azure Storage.

![][1]

*Rysunek 1 monitorowania i diagnostyki i rozwiązywania problemów*

Ten przewodnik jest zamierzone toobe odczytu głównie przez deweloperów usług online, korzystających z usług magazynu Azure i specjalistów IT jest odpowiedzialny za zarządzanie takich usług online. Witaj cele tego przewodnika są:

* toohelp Obsługa hello kondycji i wydajności konta magazynu Azure.
* tooprovide program hello niezbędne procesów i narzędzi toohelp zdecydować, czy problem w aplikacji lub problem dotyczy tooAzure magazynu.
* tooprovide z możliwością wykonania akcji wskazówki dotyczące rozwiązywania problemów związanych z tooAzure magazynu.

### <a name="how-this-guide-is-organized"></a>Jak jest zorganizowana w tym przewodniku
Witaj w sekcji "[monitorowania usługi magazynu]" w tym artykule opisano, jak toomonitor hello kondycji i wydajności usługi Magazyn Azure przy użyciu metryk aplikacji usługi Azure Storage Analytics (metryk Storage).

Witaj sekcji "[diagnozowanie problemów z magazynowaniem]" w tym artykule opisano, jak problemy toodiagnose korzystania z usługi Azure magazynu Analytics rejestrowania (rejestrowania magazynu). Opisuje również sposób tooenable rejestrowania po stronie klienta przy użyciu hello urządzeń w jednej z bibliotek klienta hello, takich jak hello biblioteki klienta usługi Storage dla platformy .NET lub hello Azure SDK dla języka Java.

Witaj w sekcji "[śledzenia End-to-end]" w tym artykule opisano, jak można skorelować hello informacje zawarte w różnych plikach dziennika i dane metryk.

Witaj w sekcji "[wskazówki rozwiązywania problemów]" znajdują się wskazówki dotyczące rozwiązywania problemów w przypadku niektórych hello typowe związane z magazynowaniem problemy mogą wystąpić.

Witaj "[dodatki]" zawierają informacje o przy użyciu innych narzędzi, takich jak Wireshark i Netmon analizowanie sieci pakietów danych, narzędzia Fiddler do analizowania komunikaty HTTP/HTTPS, a dane dziennika programu Microsoft Message Analyzer dla korelacji.

## <a name="monitoring-your-storage-service"></a>Monitorowanie usługi magazynu
Jeśli znasz monitorowania wydajności systemu Windows, można traktować metryki magazynu jako odpowiednik liczników monitora wydajności systemu Windows Azure Storage. Metryki magazynu zawiera rozbudowany zestaw metryki (liczniki w terminologii Monitor wydajności systemu Windows), np. dostępność usługi, całkowita liczba żądań tooservice lub odsetek pomyślnych żądań tooservice (Aby uzyskać pełną listę hello dostępne metryki, zobacz <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">schemat tabeli metryki analityka magazynu</a> w witrynie MSDN). Można określić, czy mają hello magazynu usługi toocollect i agregacji metryki co godzinę lub co minutę. Aby uzyskać więcej informacji na temat tooenable metryk i monitorowanie kont magazynu, zobacz temat <a href="http://go.microsoft.com/fwlink/?LinkId=510865" target="_blank">Włączanie metryk storage</a> w witrynie MSDN.

Można wybrać, które metryki co godzinę ma toodisplay w hello Azure Classic Portal i skonfigurować reguły powiadamiania administratorów za pośrednictwem poczty e-mail, gdy metryki co godzinę przekracza próg określonego (Aby uzyskać więcej informacji, zobacz stronę hello <a href="http://msdn.microsoft.com/library/azure/dn306638.aspx" target="_blank">jak: Odbieranie powiadomień o alertach i zarządzać nimi reguł alertów na platformie Azure</a>). Usługa magazynu Hello zbiera metryki przy użyciu podjęto najlepsze możliwe działanie, ale nie można rejestrować każdej operacji magazynu.

Na rysunku 2 poniżej przedstawiono hello monitorowania strony w hello klasycznego portalu Azure, gdzie można przeglądać metryki, np. dostępność, całkowita liczba żądań i numery Średni czas oczekiwania dla konta magazynu. Reguły powiadomień został również skonfigurowany tooalert administrator Jeśli dostępności spadnie poniżej określonego poziomu. Wyświetlanie te dane, jednego obszaru możliwych do badania jest hello tabeli usługi procent powodzenia trwa poniżej 100% (Aby uzyskać więcej informacji, zobacz sekcję hello "[metryki pokazują PercentSuccess niskim lub wpisy dziennika analizy zawierać operacje z Stan transakcji ClientOtherErrors]").

![][2]

*Rysunek 2 wyświetlania metryk pamięci masowej w hello klasycznego portalu Azure*

Należy monitorować stale tooensure z aplikacjami platformy Azure, są one dobrej kondycji i wydajności, zgodnie z oczekiwaniami:

* Ustanawianie niektóre metryki linii bazowej dla aplikacji, które będą pozwalają toocompare bieżące dane i identyfikację wszelkich istotnych zmian w zachowanie hello magazynu Azure i aplikacji. w wielu przypadkach Hello wartości metryki z linii bazowej będzie określone dla aplikacji i należy je określić w przypadku testowania aplikacji.
* Rejestrowanie minuty metryki i ich użycie toomonitor aktywnie nieoczekiwane błędy i anomalie, takich jak gwałtowny wzrost liczby błędów lub liczby żądań.
* Rejestrowanie metryki co godzinę i ich użycie wartości średnie toomonitor takie jak średni liczby błędów i liczby żądań.
* Badania potencjalnych problemów za pomocą narzędzi diagnostycznych, zgodnie z opisem w dalszej części hello "[diagnozowanie problemów z magazynowaniem]."

Wykresy Hello na rysunku 3 poniżej pokazują, jak hello uśrednianie występujący dla metryki co godzinę można ukryć wzrostów w działaniu. metryki co godzinę Hello są wyświetlane tooshow stała liczba żądań, podczas minutę hello metryki ujawnić wahań hello, które naprawdę odbywają się.

![][3]

Witaj pozostałej części tej sekcji opisano metryki, które należy monitorować i dlaczego.

### <a name="monitoring-service-health"></a>Monitorowanie kondycji usługi
Można użyć hello [klasycznego portalu Azure](https://manage.windowsazure.com) regiony platformy Azure wokół hello world hello tooview hello kondycji usługi magazynu hello (i innych usług Azure) we wszystkich. Dzięki temu możesz toosee natychmiast Jeśli problemu poza formantu ma wpływ na powitania usługi magazynu w regionie hello, używane w przypadku aplikacji.

Witaj klasycznego portalu Azure może także udostępnić powiadomienia zdarzenia mające wpływ na powitania różne usługi platformy Azure.
Uwaga: Te informacje wcześniej była dostępna, wraz z danych historycznych, na hello pulpicie nawigacyjnym usługi Azure w <a href="http://status.azure.com" target="_blank">http://status.azure.com</a>.

Gdy hello klasycznego portalu Azure zbiera informacje o kondycji z wewnątrz hello centrach danych platformy Azure (poza wewnątrz monitorowanie), możesz również przyjęcie podejścia w zewnętrznej toogenerate transakcji syntetycznych, które okresowo dostęp do Twojego hostowanymi na platformie Azure Aplikacja sieci Web z wielu lokalizacji. Witaj usług oferowanych przez <a href="http://www.keynote.com/solutions/monitoring/web-monitoring" target="_blank">prelekcji</a>, <a href="https://www.gomeznetworks.com/?g=1" target="_blank">Gomez</a>, i przykłady tego podejścia zewnętrznej usługi Application Insights dla programu Visual Studio Team Services. Aby uzyskać więcej informacji dotyczących usługi Application Insights dla programu Visual Studio Team Services, zobacz dodatek hello "[dodatek 5: monitorowanie za pomocą usługi Application Insights dla programu Visual Studio Team Services]."

### <a name="monitoring-capacity"></a>Monitorowanie wydajności
Metryki magazynu przechowuje dane tylko metryki pojemności dla usługi blob hello ponieważ obiekty BLOB zwykle konta hello największą część przechowywanych danych (w czasie hello zapisu, nie jest możliwe toouse metryki magazynu toomonitor hello pojemność tabel i kolejek) . Te dane można znaleźć w hello **$MetricsCapacityBlob** tabeli, jeśli jest włączone monitorowanie hello usługi Blob. Metryki magazynu rejestruje dane raz dziennie, i można użyć wartości hello hello **RowKey** toodetermine czy hello wiersz zawiera jednostki, która odnosi się toouser danych (wartość **danych**) lub analizy danych ( wartość **analytics**). Każdej jednostki przechowywanej zawiera informacje o hello ilość użytego magazynu (**pojemności** mierzony w bajtach), a bieżąca liczba kontenerów hello (**ContainerCount**) i obiektów blob ( **ObjectCount**) używanych w hello konta magazynu. Aby uzyskać więcej informacji o metryki pojemności hello przechowywane w hello **$MetricsCapacityBlob** tabeli, zobacz <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">schemat tabeli metryki analityka magazynu</a> w witrynie MSDN.

> [!NOTE]
> Należy monitorować te wartości wczesne ostrzeżenie, że zbliża się hello limitu pojemności konta magazynu. W hello klasycznego portalu Azure na powitania **Monitor** strony dla konta magazynu, można dodać alert toonotify reguły, jeśli użycie agregacji magazynu przekracza lub spadnie poniżej określonych progów.
> 
> 

Trwa szacowanie rozmiaru hello różnych obiektów pamięci masowej, takich jak obiekty BLOB pomoc na ten temat można znaleźć w blogu hello <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx" target="_blank">opis Azure magazynu rozliczeń — przepustowość, transakcje i pojemności</a>.

### <a name="monitoring-availability"></a>Monitorowanie dostępności
Należy monitorować hello dostępności usług magazynu hello na koncie magazynu przez wartość hello w hello monitorowania **dostępności** kolumny w hello godzinowe i minutowe metryki tabel — **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Witaj **dostępności** kolumna zawiera wartość procentową, która wskazuje hello dostępności usługi hello lub reprezentowanego przez wiersz hello operacji hello interfejsu API (hello **RowKey** pokazuje, czy wiersz hello zawiera metryki dla usługi hello jako całość lub dla określonej operacji interfejsu API).

Wszystkie wartości mniejszej niż 100% wskazuje, że niektóre żądania magazynu kończą się niepowodzeniem. Widać, dlaczego ulegają awarii, sprawdzając hello innych kolumn danych metryki hello takich jak Pokaż hello liczby żądań z typami inny błąd **ServerTimeoutError**. Należy oczekiwać toosee **dostępności** spadek tymczasowo poniżej 100% powodów takich, jak limity czasu przejściowa serwera podczas usługi hello przenosi partycje toobetter Równoważenie obciążenia żądania; hello ponów logikę w aplikacji klienta powinna obsługiwać takie warunki tymczasowymi. Strona Hello <a href="http://msdn.microsoft.com/library/azure/hh343260.aspx" target="_blank"> </a> list hello typów transakcji, które zawiera metryki magazynu w jego **dostępności** obliczeń.

W hello klasycznego portalu Azure na powitania **Monitor** strony dla konta magazynu, można dodać reguły alertów toonotify możesz Jeśli **dostępności** dla usługi spadnie poniżej progu, który określisz.

Witaj "[wskazówki rozwiązywania problemów]" sekcji tego przewodnika opisano niektóre typowe magazynu usługi problemów powiązanych tooavailability.

### <a name="monitoring-performance"></a>Monitorowanie wydajności
wydajność hello toomonitor hello usług magazynu, można użyć hello poniższych metryki z hello co godzinę i minuty metryki tabel.

* Witaj wartości hello **AverageE2ELatency** i **AverageServerLatency** Pokaż hello Średni czas hello magazynu usługi lub typ operacji interfejsu API trwa tooprocess żądań. **AverageE2ELatency** jest miarą end-to-end opóźnienia, które obejmuje czas hello tooread hello żądania i wysyła odpowiedź hello w tooprocess hello prośbę o dodanie toohello czas trwania (w związku z tym obejmuje opóźnienia sieci po hello żądania osiągnie usługi magazynu hello); **AverageServerLatency** to miara tylko hello czas przetwarzania i dlatego nie obejmuje opóźnienia sieci, wszystkie powiązane toocommunicating powitania klienta. Witaj w sekcji "[metryki pokazują AverageE2ELatency wysoki i niski AverageServerLatency]" w dalszej części tego przewodnika, aby uzyskać informacje dotyczące przyczyny może występować znaczące różnice między tymi dwoma wartościami.
* Witaj wartości hello **TotalIngress** i **TotalEgress** kolumny zawierają hello łączna ilość danych, w bajtach przychodzących tooand przechodzi poza usługą magazynu lub za pomocą określonego typu operacji interfejsu API.
* Witaj wartości hello **TotalRequests** otrzymuje kolumny Pokaż hello całkowita liczba żądań, które hello usługi magazynu operacji interfejsu API. **TotalRequests** hello łączna liczba żądań, które otrzymuje hello usługi magazynu.

Zazwyczaj monitorujesz nieoczekiwane zmiany w dowolnej z tych wartości jako wskaźnik, czy masz wymagane jest zbadanie problemu.

W hello klasycznego portalu Azure na powitania **Monitor** strony dla konta magazynu, można dodać reguły alertów toonotify Jeśli żadnego hello metryki wydajności dla tej usługi spadną poniżej lub przekracza wartość progową, który określisz.

Witaj "[wskazówki rozwiązywania problemów]" sekcji tego przewodnika opisano niektóre typowe magazynu usługi problemów powiązanych tooperformance.

## <a name="diagnosing-storage-issues"></a>Diagnozowanie problemów z magazynowaniem
Istnieje wiele sposobów, czy użytkownik może zostaną powiadomieni o problem lub problem w aplikacji, należą:

* Poważnej awarii powoduje, że aplikacja hello toocrash lub toostop działać.
* Znaczące zmiany z linii bazowej wartości metryk hello monitorowania zgodnie z opisem w poprzedniej sekcji hello "[monitorowania usługi magazynu]."
* Raporty z użytkowników aplikacji, że niektóre określonej operacji nie została ukończona, zgodnie z oczekiwaniami lub nie działa niektórych funkcji.
* Błędy wygenerowane w aplikacji pojawiających się w plikach dziennika lub za pomocą innej metody powiadomień.

Zazwyczaj usług magazynu powiązanych tooAzure problemy należą do jednej z czterech szerokie kategorie:

* Aplikacja ma problem z wydajnością, zgłoszone przez użytkowników albo ujawniony z powodu zmian w hello metryki wydajności.
* Występuje problem z infrastrukturą usługi Azure Storage hello w jeden lub więcej regionów.
* Aplikacja napotyka błąd zgłoszony przez użytkowników albo ujawniony przez zwiększenie w jednym z hello błąd liczby metryk, które należy monitorować.
* Podczas projektowania i testowania może używać hello lokalnym emulatorze magazynu; mogą wystąpić problemy, które odnoszą się w szczególności toousage hello emulatora magazynu.

Witaj poniższych sekcjach podano hello kroki należy wykonać toodiagnose i rozwiązywania problemów w każdej z tych czterech kategorii. Witaj w sekcji "[wskazówki rozwiązywania problemów]" dalszej części tego podręcznika zawiera więcej szczegółów dla niektórych typowych problemów, które mogą wystąpić.

### <a name="service-health-issues"></a>Problemy z usługi kondycji
Problemy z usługi kondycji są zazwyczaj poza formantu. Hello klasyczny Portal Azure udostępnia informacje dotyczące bieżących problemów z usługami Azure, takich jak usługi magazynu. Jeśli zostanie wybrana opcja dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu podczas tworzenia konta magazynu, następnie w zdarzeniu hello danych są niedostępne w lokalizacji głównej hello, aplikację można przełączyć tymczasowo toohello kopia tylko do odczytu w lokalizacji dodatkowej hello. toodo, aplikacja musi być możliwe tooswitch między przy użyciu lokalizacji magazynów podstawowych i pomocniczych hello, a stanie toowork w tryb zmniejszonej funkcjonalności danych tylko do odczytu. biblioteki klienta magazynu Azure Hello pozwalają toodefine zasady ponawiania, który może odczytywać dane z magazynu pomocniczego w przypadku błędu odczytu z magazynu głównego. Aplikacja musi również pamiętać, że hello danych w dodatkowej lokalizacji hello jest ostatecznie spójne toobe. Aby uzyskać więcej informacji, zobacz hello blogu <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/04/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx" target="_blank">opcje nadmiarowość magazynu Azure i dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu</a>.

### <a name="performance-issues"></a>Problemy z wydajnością
Witaj wydajności aplikacji może być subiektywne, szczególnie z punktu widzenia użytkownika. Dlatego jest ważne toohave linii bazowej metryki dostępności toohelp należy określić w przypadku, gdy może być problem z wydajnością. Wiele czynników może wpłynąć na wydajność hello usługi magazynu platformy Azure z perspektywy aplikacji hello klienta. Te czynniki mogą działać w usłudze magazynowania hello, powitania klienta lub hello infrastruktury sieci. Dlatego jest ważne toohave strategii identyfikowanie hello pochodzenia hello problem z wydajnością.

Po zidentyfikowaniu hello lokalizacji prawdopodobnie Przyczyna hello hello problemu z wydajnością z hello metryki mogą być następnie toofind pliki dziennika hello Użyj szczegółowe informacje o toodiagnose i dalsze hello problemu.

Witaj w sekcji "[wskazówki rozwiązywania problemów]" dalszej części tego podręcznika zawiera więcej informacji na temat niektórych typowych wydajności związane z problemów, które mogą wystąpić.

### <a name="diagnosing-errors"></a>Diagnozowanie błędów
Użytkownicy aplikacji mogą informować o błędów zgłoszonych przez aplikację klienta hello. Takie jak magazyn metryki liczby typów inny błąd z usług magazynu rejestruje także **NetworkError**, **ClientTimeoutError**, lub **AuthorizationError**. Gdy metryki magazynu rejestruje tylko liczby o różnych typów, można uzyskać szczegółowe informacje o poszczególnych żądań, przeglądając po stronie serwera, po stronie klienta oraz dzienniki sieci. Zazwyczaj zwrócony przez usługę magazynu hello kod stanu HTTP hello zapewni wskazanie Dlaczego hello żądanie nie powiodło się.

> [!NOTE]
> Należy pamiętać, że należy oczekiwać toosee sporadyczne błędy: na przykład błędy powodu warunków sieciowych tootransient lub błędów aplikacji.
> 
> 

Hello są przydatne w przypadku opis kodów stanu i błędów związane z magazynowaniem następujące zasoby w witrynie MSDN:

* <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">Typowe kody błędów interfejsu API REST</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179439.aspx" target="_blank">Kody błędów usługi blob</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179446.aspx" target="_blank">Kody błędów usługi kolejki</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179438.aspx" target="_blank">Kody błędów usługi tabel</a>

### <a name="storage-emulator-issues"></a>Problemy z emulatora magazynu
Witaj zestawu Azure SDK zawiera emulator magazynu, które można uruchamiać na deweloperskiej stacji roboczej. Emulator tego symuluje większość zachowanie hello hello usług magazynu Azure i jest przydatne podczas programowania i testowania, umożliwiając toorun aplikacji, które korzystają z usług magazynu platformy Azure bez hello wymagane dla subskrypcji platformy Azure i konto magazynu platformy Azure.

Witaj "[wskazówki rozwiązywania problemów]" sekcji tego przewodnika opisano typowe problemy napotkano przy użyciu emulatora magazynu hello.

### <a name="storage-logging-tools"></a>Narzędzia rejestrowania magazynu
Rejestrowanie magazynu zapewnia po stronie serwera rejestrowanie żądań magazynu na koncie magazynu Azure. Aby uzyskać więcej informacji dotyczących sposobu rejestrowania po stronie serwera tooenable i hello dostępu rejestrowanie danych, zobacz <a href="http://go.microsoft.com/fwlink/?LinkId=510867" target="_blank">przy użyciu rejestrowania po stronie serwera</a> w witrynie MSDN.

Witaj biblioteki klienta usługi Storage dla platformy .NET umożliwia danych dziennika klienta toocollect odnosi się toostorage operacje wykonywane przez aplikację. Aby uzyskać więcej informacji dotyczących sposobu rejestrowania po stronie klienta tooenable i hello dostępu rejestrowanie danych, zobacz <a href="http://go.microsoft.com/fwlink/?LinkId=510868" target="_blank">rejestrowania po stronie klienta przy użyciu hello biblioteki klienta usługi Storage</a> w witrynie MSDN.

> [!NOTE]
> W niektórych sytuacjach (np. awarii autoryzacji sygnatury dostępu Współdzielonego) użytkownik może zgłosić błąd, który można znaleźć żadnych danych żądania w hello dzienniki magazynu po stronie serwera. Możesz użyć możliwości rejestrowania hello tooinvestigate biblioteki klienta usługi Storage hello Jeśli hello przyczyny problemu hello znajduje się na powitania klienta lub narzędzia tooinvestigate hello sieci do monitorowania sieci.
> 
> 

### <a name="using-network-logging-tools"></a>Przy użyciu narzędzia rejestracji w sieci
Można przechwytywać ruch hello między powitania klienta i serwera tooprovide szczegółowe informacje o hello danych powitania klienta i serwera są wymiana i hello podstawowych warunków sieciowych. Narzędzia rejestrowania przydatne sieci obejmują:

* Fiddler (<a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>) to bezpłatne sieci web profilowanie serwera proxy, który pozwala tooexamine hello nagłówki i danych ładunku komunikatów żądań i odpowiedzi HTTP i HTTPS. Aby uzyskać więcej informacji, zobacz "[dodatku 1: ruchu HTTP i HTTPS toocapture przy użyciu narzędzia Fiddler]".
* Monitor sieci firmy Microsoft (Netmon) (<a href="http://www.microsoft.com/download/details.aspx?id=4865" target="_blank">http://www.microsoft.com/download/details.aspx?id=4865</a>) i programu Wireshark (<a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>) są analizatorów protokołu, które umożliwiają wolnej sieci Możesz tooview szczegółowe informacje pakietu dla szerokiego zakresu protokołów sieciowych. Aby uzyskać więcej informacji na temat programu Wireshark, zobacz "[dodatek 2: ruchu sieciowego przy użyciu programu Wireshark toocapture]".
* Programu Microsoft Message Analyzer to narzędzie firmy Microsoft, który zastępuje Monitor sieci oraz dodatkowo toocapturing sieci danych pakietu, pomaga tooview i analizować dane dzienników hello przechwytywane z innych narzędzi. Aby uzyskać więcej informacji, zobacz "[dodatku 3: ruchu sieciowego przy użyciu programu Microsoft Message Analyzer toocapture]".
* Jeśli chcesz tooperform toocheck test podstawowej łączności, komputerze klienckim połączyć z usługą magazynu platformy Azure toohello hello sieci, nie możesz tego zrobić przy użyciu standardu hello **ping** narzędzia na powitania klienta. Można jednak użyć hello **tcping** narzędzia toocheck łączności. **Tcping** jest dostępny do pobrania na <a href="http://www.elifulkerson.com/projects/tcping.php" target="_blank">http://www.elifulkerson.com/projects/tcping.php</a>.

W wielu przypadkach hello danych dziennika z rejestrowania magazynu i biblioteki klienta usługi Storage hello będą wystarczające toodiagnose problemu, ale w niektórych scenariuszach może być konieczne hello bardziej szczegółowe informacje, które zapewniają te narzędzia rejestrowania w sieci. Na przykład przy użyciu narzędzia Fiddler tooview HTTP i HTTPS umożliwia wiadomości tooview nagłówka i ładunku danych wysłanych tooand z hello usługi magazynu, które umożliwiłyby możesz tooexamine jak aplikacja kliencka ponowi próbę operacji magazynu. Protokół analizatorów, takich jak Wireshark działają na poziomie pakietów hello, umożliwiając tooview TCP danych, które umożliwią tootroubleshoot utraty pakietów i problemy z łącznością. Message Analyzer może działać z warstwy protokołów HTTP i TCP.

## <a name="end-to-end-tracing"></a>Śledzenia end-to-end
Przy użyciu różnych plikach dziennika śledzenia end-to-end to technika przydatne do badania potencjalnych problemów. Jako oznaczenie, w którym toostart wyszukiwania w plikach dziennika hello hello szczegółowe informacje, które zawierają informacje pomocne podczas rozwiązywania problemu hello służy hello informacji daty i godziny od danych metryki.

### <a name="correlating-log-data"></a>Korelowanie dane dziennika
Podczas wyświetlania dzienniki za pośrednictwem aplikacji klienckich, śledzi sieci i magazynu po stronie serwera, rejestrowanie go krytyczne toobe toocorrelate stanie żądania całej hello różnych plikach dziennika. pliki dziennika Hello obejmują szereg różnych pól, które są przydatne jako identyfikatorów korelacji. Identyfikator żądania klienta Hello jest hello najbardziej przydatne pola toouse toocorrelate wpisów w różnych dzienników hello. Jednak czasami może być przydatne toouse identyfikator żądania serwera hello lub sygnatur czasowych. Witaj poniższe sekcje zawierają więcej informacji na temat tych opcji.

### <a name="client-request-id"></a>Identyfikator żądania klienta
Witaj biblioteki klienta usługi Storage automatycznie generuje identyfikator żądania klienta unikatowy dla każdego żądania.

* W hello dziennika po stronie klienta, który hello biblioteki klienta usługi Storage tworzy, identyfikator żądania klienta hello jest wyświetlana w hello **Identyfikatora żądania klienta** pola każdego wpisu dziennika dotyczących toohello żądania.
* W śledzenia sieci, takiej jak przechwycone przez Fiddler, identyfikator żądania klienta hello jest widoczna w komunikaty żądania jako hello **x-ms-client żądania id** wartość nagłówka HTTP.
* W dzienniku rejestrowania magazynu po stronie serwera hello identyfikatora żądania klienta hello pojawia się w kolumnie identyfikator żądania klienta hello.

> [!NOTE]
> Możliwe jest dla wielu żądań tooshare hello tego samego identyfikatora żądania klienta, ponieważ powitania klienta można przypisać wartości (chociaż hello biblioteki klienta usługi Storage automatycznie przypisuje nową wartość). W przypadku hello ponownych prób z powitania klienta, wszystkie próby udostępniać hello tego samego identyfikatora żądania klienta. W przypadku hello partii wysłane przez klienta na powitania partii hello ma identyfikator żądania jednego klienta.
> 
> 

### <a name="server-request-id"></a>Identyfikator żądania serwera
Usługa Magazyn Hello automatycznie generuje identyfikatorów żądania serwera.

* W dzienniku rejestrowania magazynu po stronie serwera hello identyfikator żądania serwera hello pojawia się hello **nagłówka Identyfikatora żądania** kolumny.
* W śledzenia sieci, takiej jak przechwycone przez Fiddler, identyfikator żądania serwera hello pojawia się w wiadomości odpowiedzi jako hello **x-ms-request-id** wartość nagłówka HTTP.
* W hello dziennika po stronie klienta, który hello biblioteki klienta usługi Storage tworzy, identyfikator żądania serwera hello jest wyświetlana w hello **tekst operacji** kolumny dla wpisu dziennika hello zawierającego szczegóły hello odpowiedź serwera.

> [!NOTE]
> Usługa Magazyn Hello zawsze przypisuje unikatowy serwera żądania identyfikator tooevery odebrane żądanie, co ponowienia próby z powitania klienta i każda operacja wchodzące w skład partii ma identyfikator żądania serwera unikatowy.
> 
> 

Jeśli hello biblioteki klienta usługi Storage zgłasza **StorageException** w kliencie hello hello **RequestInformation** właściwość zawiera **RequestResult** obiekt, który zawiera **ServiceRequestID** właściwości. Można także przejść do **RequestResult** obiekt z **elementu OperationContext** wystąpienia.

Hello poniższy przykład kodu pokazuje sposób tooset niestandardowego **ClientRequestId** wartość dołączając **elementu OperationContext** obiekt hello żądania toohello magazynu usługi. Zawiera także sposób tooretrieve hello **ServerRequestId** wartość z zakresu od hello komunikat odpowiedzi.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Znaczniki czasu
Można również użyć sygnatury czasowe toolocate powiązane wpisy dziennika, ale należy zwrócić szczególną uwagę na dowolnym zegara między powitania klienta i serwera, który może istnieć. Powinna przeszukać plus lub minus 15 minut do dopasowania wpisów po stronie serwera w oparciu sygnatury czasowej hello na powitania klienta. Należy pamiętać, że metadane obiektu blob hello hello obiektów blob zawierający metryki wskazuje hello zakres czasu dla metryki hello przechowywane w obiekcie blob hello; jest to przydatne, jeśli masz wiele metryki obiektów blob dla hello tego samego minutę lub godzinę.

## <a name="troubleshooting-guidance"></a>Wskazówki dotyczące rozwiązywania problemów
Ta sekcja pomoże Ci na powitania diagnozowania i rozwiązywania niektórych typowych problemów z hello aplikacji mogą wystąpić podczas korzystania z usług magazynu Azure hello. Użyj listy hello poniżej toolocate hello informacje istotne tooyour określonego problemu.

**Rozwiązywanie problemów z drzewa decyzyjnego**

- - -
Problem związek toohello wykonanie jednej z usług magazynu hello?

* [metryki pokazują AverageE2ELatency wysoki i niski AverageServerLatency]
* [Metryki pokazują AverageE2ELatency niski i niski AverageServerLatency, ale występuje duże opóźnienie powitania klienta]
* [Metryki wskazują wysoką wartość AverageServerLatency]
* [Występują nieoczekiwane opóźnienia w dostarczaniu komunikatów w kolejce]

- - -
Problem związek dostępności toohello jednej z usług magazynu hello?

* [metryki spowodować wzrost PercentThrottlingError]
* [metryki spowodować wzrost PercentTimeoutError]
* [Metryki wskazują wzrost wartości PercentNetworkError]

- - -
Aplikacja kliencka odbiera odpowiedź HTTP 4XX (na przykład 404) z usługą magazynu?

* [powitania klienta odbiera komunikaty HTTP 403 (Dostęp zabroniony)]
* [powitania klienta odbiera komunikaty HTTP 404 (nie znaleziono)]
* [powitania klienta odbiera komunikaty HTTP 409 (konflikt)]

- - -
[metryki pokazują PercentSuccess niskim lub wpisy dziennika analizy zawierać operacje z Stan transakcji ClientOtherErrors]

- - -
[Metryki pojemności Pokaż nieoczekiwane zwiększenie wykorzystania pojemności magazynu]

- - -
[Występują nieoczekiwane ponowne uruchomienie maszyn wirtualnych, które mają wiele wirtualnych dysków twardych dołączonych]

- - -
[Problem wynika z przy użyciu emulatora magazynu hello do rozwoju lub testu]

- - -
[Pojawiły się problemy z instalacją hello Azure SDK dla platformy .NET]

- - -
[Inny problem z usługą magazynu]

- - -
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Metryki pokazują AverageE2ELatency wysoki i niski AverageServerLatency
Witaj bNiski ilustracji z narzędzia monitorowania klasycznego portalu Azure hello przedstawiono przykład gdzie hello **AverageE2ELatency** jest znacznie wyższa niż hello **AverageServerLatency**.

![][4]

Należy pamiętać, że Usługa magazynu hello tylko oblicza metrykę hello **AverageE2ELatency** pomyślnych żądań oraz, w odróżnieniu od **AverageServerLatency**, zawiera czasie powitania klienta hello toosend hello dane i otrzymywać potwierdzenia hello usługi magazynu. W związku z tym różnica między **AverageE2ELatency** i **AverageServerLatency** może być albo powodu toohello klienta aplikacji jest powolne toorespond lub z powodu tooconditions hello sieci.

> [!NOTE]
> Można również wyświetlić **E2ELatency** i **ServerLatency** dane dziennika dla poszczególnych magazynu operacji w hello rejestrowania magazynu.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Do badania problemów dotyczących wydajności klienta
Możliwe przyczyny powitania klienta wolno odpowiadać obejmują o ograniczonej liczby dostępnych połączeń i wątków. Może być problem hello stanie tooresolve, modyfikując powitania klienta kodu toobe bardziej wydajne (na przykład za pomocą usługi magazynu toohello wywołania asynchroniczne) lub przy użyciu większe maszyny wirtualnej (z większej liczby rdzeni i ilości dostępnej pamięci).

Hello usług tabeli i kolejki, algorytm Nagle'a hello może również spowodować wysokiej **AverageE2ELatency** w porównaniu zbyt**AverageServerLatency**: Aby uzyskać więcej informacji, zobacz hello post <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx" target="_blank">Nagle'a firmy Algorytm jest nie przyjazną kierunku małych żądań</a> na powitania Blog zespołu usługi Magazyn Microsoft Azure. Algorytm Nagle'a hello w kodzie można wyłączyć za pomocą hello **ServicePointManager —** klasy w hello **System.Net** przestrzeni nazw. Ten krok należy wykonać przed wprowadzasz tabeli toohello wywołania lub usługi kolejki w aplikacji, ponieważ nie dotyczy to połączeń znajdujących się już otworzyć. Witaj poniższy przykład pochodzi z hello **Application_Start** metody w roli procesu roboczego.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Należy sprawdzić powitania klienta dzienniki toosee ile aplikacja kliencka jest przesyłanie żądań i sprawdź, czy ogólne .NET powiązane wąskich gardeł wydajności w sieci klienta, takie jak procesor CPU, pamięci .NET, wykorzystania sieci lub pamięci (jako początkowy Rozwiązywanie problemów z aplikacjami klienta .NET w punkcie, zobacz <a href="http://msdn.microsoft.com/library/7fe0dd2y(v=vs.110).aspx" target="_blank">debugowanie, śledzenie i profilowanie</a> w witrynie MSDN).

#### <a name="investigating-network-latency-issues"></a>Badanie problemów z opóźnieniem w sieci
Zazwyczaj duże opóźnienie end-to-end spowodowane sieci hello jest powodu tootransient warunki. Zarówno problemy z siecią przejściowych i trwałe takich jak porzuconych pakietów można zbadać za pomocą narzędzi takich jak Wireshark lub programu Microsoft Message Analyzer.

Aby uzyskać więcej informacji o korzystaniu z programu Wireshark tootroubleshoot sieci problemów, zobacz "[dodatek 2: ruchu sieciowego przy użyciu programu Wireshark toocapture]."

Aby uzyskać więcej informacji o korzystaniu z programu Microsoft Message Analyzer tootroubleshoot sieci problemów, zobacz "[dodatku 3: ruchu sieciowego przy użyciu programu Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Metryki pokazują AverageE2ELatency niski i niski AverageServerLatency, ale występuje duże opóźnienie powitania klienta
W tym scenariuszu hello najbardziej prawdopodobną przyczyną jest opóźnienia w żądań magazynu hello osiągnięcia hello usługi magazynu. Należy zbadać, dlaczego żądania z klienta na powitania nie dokonywania go za pośrednictwem usługi blob toohello.

Możliwe przyczyny powitania klienta opóźnienie wysyłania żądań obejmują o ograniczonej liczby dostępnych połączeń i wątków. Należy także Sprawdź, czy hello klient wykonuje wiele ponownych prób i zbadaj Przyczyna hello przypadku hello. Można to zrobić programowo przeszukując hello **elementu OperationContext** obiekt skojarzony z hello żądania i pobierania hello **ServerRequestId** wartości. Aby uzyskać więcej informacji, zobacz hello przykładowy kod w sekcji hello "[identyfikator żądania serwera]."

Jeśli nie ma żadnych problemów w powitania klienta, powinien być sprawdzony potencjalnych problemów sieci, takich jak utraty pakietów. Można użyć narzędzia, takie jak Wireshark lub programu Microsoft Message Analyzer tooinvestigate problemy z siecią.

Aby uzyskać więcej informacji o korzystaniu z programu Wireshark tootroubleshoot sieci problemów, zobacz "[dodatek 2: ruchu sieciowego przy użyciu programu Wireshark toocapture]."

Aby uzyskać więcej informacji o korzystaniu z programu Microsoft Message Analyzer tootroubleshoot sieci problemów, zobacz "[dodatku 3: ruchu sieciowego przy użyciu programu Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-high-AverageServerLatency"></a>Metryki pokazują AverageServerLatency wysoka
W przypadku hello wysoki **AverageServerLatency** żądań pobrania obiektu blob, należy użyć hello rejestrowania magazynu rejestruje toosee, jeśli istnieją ponownego żądania hello tej samej obiektów blob (lub zestaw obiektów blob). Dla obiektu blob przesyłanie żądań, należy zbadać, jakie bloku rozmiar hello klient używa (na przykład bloki mniej niż 64 KB rozmiaru może spowodować koszty, chyba że odczytuje hello są w mniej niż 64 KB fragmentów), i jeśli wielu klientów przekazywany blokuje toohello tego samego blob równolegle. Należy także sprawdzić metryki na minutę hello maksymalnej hello liczbę żądań, które powoduje przekroczenie hello na drugi wartości docelowe skalowalności: Zobacz też "[metryki spowodować wzrost PercentTimeoutError]."

Jeśli widzisz wysokiego **AverageServerLatency** dla żądań pobierania obiektu blob podczas są powtarzane żądań hello tego samego obiektu blob lub zestaw obiektów blob, następnie należy wziąć pod uwagę buforowanie tych obiektów blob przy użyciu usługi pamięć podręczna Azure lub hello Azure Content Delivery Network (CDN). Dla żądania przesłania może zwiększyć przepływność hello za pomocą większego rozmiaru bloku. Tootables zapytania jest również możliwe tooimplement po stronie klienta pamięci podręcznej na klientach, wykonujących hello sam zapytań operacje, których hello danych nie zmieniają się często.

Wysoka **AverageServerLatency** wartości mogą też być objawem źle skonstruowane tabel lub kwerend, wynik operacji skanowania lub że skorzystaj z hello przed wzorzec Dołącz/dołączy. Zobacz "[metryki spowodować wzrost PercentThrottlingError]" Aby uzyskać więcej informacji.

> [!NOTE]
> Można znaleźć tutaj kontrolną wydajności kompleksowe Lista kontrolna: [wydajność magazynu Microsoft Azure i listę kontrolną skalowalność](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Występują nieoczekiwane opóźnienia dotyczące dostarczania wiadomości w kolejce
Jeśli występuje opóźnienie między czasu hello komunikat tooa kolejki i hello czasu staje się dostępna tooread z kolejki hello dodaje aplikację, a następnie należy wykonać następujące kroki toodiagnose hello problem hello:

* Sprawdź, czy aplikacja hello pomyślnie polega na dodaniu kolejka toohello wiadomości powitania. Sprawdź, czy aplikacja hello nie ponawia hello **AddMessage** metody kilka razy przed pomyślne. Dzienniki biblioteki klienta usługi Storage Hello zostaną wyświetlone wszystkie kolejne próby operacji magazynu.
* Sprawdź, czy nie istnieje żaden zegar pochylenia między roli procesu roboczego hello dodające kolejki toohello wiadomość hello i roli proces roboczy hello odczytujący hello wiadomości z kolejki hello, który ułatwia są wyświetlane tak, jakby to opóźnienie podczas przetwarzania.
* Sprawdź, czy rola proces roboczy hello odczytujący wiadomości powitania od hello kolejki jest możliwe. Jeśli klient kolejki wywołuje hello **GetMessage** metoda zawiedzie ale toorespond z potwierdzeniem, wiadomość hello pozostanie niewidoczny w kolejce hello do hello **invisibilityTimeout** okresu. W tym momencie wiadomość hello staje się dostępna do przetwarzania ponownie.
* Sprawdź, czy hello długość kolejki rośnie w czasie. Może to wystąpić, jeśli nie masz wystarczających tooprocess dostępne pracowników wszystkie hello wiadomości, że innych pracowników są umieszczenie w kolejce hello. Należy także sprawdzić toosee metryki hello Jeśli usunięciu żądania kończą się niepowodzeniem i hello usuwania z kolejki liczba wiadomości, które mogą wskazywać powtarzane wiadomość hello toodelete nieudanych prób.
* Przeanalizuj dzienniki hello rejestrowania magazynu dla wszystkich operacji kolejki, które mają wyższe niż oczekiwano **E2ELatency** i **ServerLatency** wartości przez dłuższy okres czasu niż zwykle.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Metryki spowodować wzrost PercentThrottlingError
Ograniczenia przepustowości błędy występują w przypadku przekroczenia wartości docelowe skalowalności hello usługi magazynu. Usługa Magazyn Hello jest to tooensure nie jednego klienta lub dzierżawcy, można użyć usługi hello na powitania koszt innych osób. Aby uzyskać więcej informacji, zobacz <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">cele dotyczące wydajności i skalowalności magazynu Azure</a> szczegółowe informacje o wartości docelowe skalowalności w przypadku kont magazynu i cele wydajności dla partycji w ramach konta magazynu.

Jeśli hello **PercentThrottlingError** Metryka spowodować wzrost hello odsetek żądań, które kończą się niepowodzeniem z powodu błędu ograniczania przepustowości, należy tooinvestigate jednego z dwóch scenariuszy:

* [Przejściowa wzrost PercentThrottlingError]
* [Stałe zwiększanie PercentThrottlingError błąd]

Wzrost **PercentThrottlingError** często występuje na powitania tej samej czasu jako wzrost hello liczba żądań magazynu lub gdy początkowo załadować testowania aplikacji. To może również manifestu sam powitania klienta jako "503 serwera zajęty" lub "500 limit czasu operacji" HTTP komunikaty o stanie operacji magazynu.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Przejściowa wzrost PercentThrottlingError
Jeśli widzisz nagłego wartości hello **PercentThrottlingError** który pokrywa się z okresy intensywnego działania aplikacji hello, należy zaimplementować wykładniczej (nie liniowej) wycofywania strategii ponownych prób w kliencie: to zmniejsza hello natychmiastowego obciążenie hello partycji i pomóc Twojej aplikacji toosmooth limit największego ruchu. Aby uzyskać więcej informacji dotyczących sposobu zasad ponawiania tooimplement przy użyciu hello biblioteki klienta usługi Storage, zobacz <a href="http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx" target="_blank">Namespace Microsoft.WindowsAzure.Storage.RetryPolicies</a> w witrynie MSDN.

> [!NOTE]
> Może również zostać wyświetlony impulsy wartości hello **PercentThrottlingError** która nie pokrywa się z okresy intensywnego działania aplikacji hello: hello tutaj najbardziej prawdopodobną przyczyną jest usługą magazynu hello przenoszenie obciążenia tooimprove partycji Równoważenie.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Stałe zwiększanie PercentThrottlingError błąd
Jeśli widzisz wysoką wartość **PercentThrottlingError** stałe wzrostu w woluminach transakcji lub wykonywania początkowej obciążenia testów dla aplikacji, a następnie należy tooevaluate jak aplikacja używa partycji magazynu i czy jej zbliża się do wartości docelowe skalowalności powitania dla konta magazynu. Na przykład jeśli widzisz ograniczania błędy w kolejce (który traktowana jako jednej partycji), następnie należy rozważyć używanie dodatkowe kolejki toospread hello transakcji między wieloma partycjami. Jeśli widzisz ograniczania błędów w tabeli, należy tooconsider przy użyciu różnych toospread schemat partycjonowania transakcje między wieloma partycjami za pomocą większej liczby wartości klucza partycji. Jeden typową przyczyną tego problemu jest hello dołączy Dołącz przed wzorzec gdzie wybierz datę hello jako klucza partycji hello, a następnie zapisywania wszystkich danych w określonym dniu partycji tooone: pod obciążeniem, może to spowodować wąskie gardło zapisu. Należy wziąć pod uwagę partycjonowania inny projekt lub oceny, czy przy użyciu magazynu obiektów blob może okazać się lepszym rozwiązaniem. Należy także sprawdzić, jeśli ograniczania hello występuje w wyniku gwałtowny wzrost ruchu i zbadaj sposobów wygładzanie deseniu żądań.

Transakcje rozpowszechniają wiele partycji, nadal należy pamiętać o limity skalowalności hello ustawione dla konta magazynu hello. Na przykład jeśli użyto kolejek dziesięć każdego przetwarzania hello maksymalnie 2000 wiadomości o rozmiarze 1KB na sekundę, będzie na powitania ogólny limit 20 000 komunikatów na sekundę dla konta magazynu hello. Jeśli potrzebujesz tooprocess ponad 20 000 jednostek na sekundę, należy rozważyć użycie wielu kont magazynu. Użytkownik powinien mieć na uwadze tego rozmiaru hello żądania i jednostek ma wpływ na kiedy usługa Magazyn hello ogranicza klientów: Jeśli masz większą żądań i jednostek może należy wcześniej ograniczany.

Projekt nieefektywne kwerendy może również spowodować limity skalowalności hello toohit do partycji tabeli. Na przykład zapytania filtru, który wybiera tylko jeden procent hello jednostek w partycji, ale która skanuje wszystkie hello jednostek w partycji należy tooaccess każdej jednostki. Każdy podmiot odczytu są zliczane hello całkowita liczba transakcji w tej partycji; w związku z tym można łatwo osiągnąć hello wartości docelowe skalowalności.

> [!NOTE]
> Testowanie wydajności powinno ujawnić żadnych projektów nieefektywne kwerendy w aplikacji.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Metryki spowodować wzrost PercentTimeoutError
Twoje metryki pokazują wzrost **PercentTimeoutError** dla jednej z usług magazynu. Na powitania sam czas, hello klient odbiera dużej liczby komunikatów o stanie "500 limit czasu operacji" HTTP z operacji magazynu.

> [!NOTE]
> Może pojawić się błędy przekroczenia limitu czasu tymczasowo jako usługa Magazyn hello żądania zrównoważenia obciążenia przez przeniesienie partycji tooa nowego serwera.
> 
> 

Witaj **PercentTimeoutError** metryka jest agregacją hello następujące metryki: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, i **SASServerTimeoutError**.

limity czasu serwera Hello są spowodowane błędem na powitania serwera. przekroczenia limitu czasu powitania klienta się tak zdarzyć, ponieważ operacji na powitania serwera przekroczyła limit czasu hello, określony przez klienta na powitania; na przykład za pomocą biblioteki klienta usługi Storage powitania klienta można ustawić czasu dla operacji przy użyciu hello **ServerTimeout** właściwości hello **QueueRequestOptions** klasy.

Limity czasu serwera wskazują na problem z usługą magazynu hello, który wymaga dalszych badań. Jeśli czy osiągnięto limity skalowalności hello hello usługi i tooidentify żadnych największego ruchu, które mogą być przyczyną tego problemu, można użyć toosee metryki. Jeśli hello problem jest przerywana, może być spowodowane równoważenia tooload aktywności w usługę hello. Jeśli hello problem jest trwałe i nie jest spowodowany przez naciśnięcie limity skalowalności hello hello usługi aplikacji, należy Zgłoś problem pomocy technicznej. Limitów czasu klienta należy zdecydować, czy limit czasu hello jest ustawiany tooan odpowiednią wartość w powitania klienta i albo zmień wartość limitu czasu hello w powitania klienta lub zbadać, jak ulepszyć wydajność hello hello operacji w usłudze magazynowania hello, dla przykład optymalizacji zapytań tabeli lub zmniejszyć rozmiar hello wiadomości.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Metryki spowodować wzrost PercentNetworkError
Twoje metryki pokazują wzrost **PercentNetworkError** dla jednej z usług magazynu. Witaj **PercentNetworkError** metryka jest agregacją hello następujące metryki: **NetworkError**, **AnonymousNetworkError**, i  **SASNetworkError**. Te wystąpić, gdy usługa Magazyn hello wykrywa błąd sieciowy hello klient wysyła żądanie magazynu.

Witaj Najczęstszą przyczyną tego błędu jest to klient rozłączanie przed upływem limitu czasu w usłudze magazynowania hello. W Twojej toounderstand klienta, kiedy i dlaczego hello klient zakończy połączenie z usługą magazynu hello powinien być sprawdzony hello kodu. Można również użyć programu Wireshark, Microsoft Message Analyzer ani Tcping tooinvestigate problemy z połączeniem sieciowym z powitania klienta. Te narzędzia są opisane w hello [dodatki].

### <a name="the-client-is-receiving-403-messages"></a>powitania klienta odbiera komunikaty HTTP 403 (Dostęp zabroniony)
Jeśli aplikacja kliencka jest zgłaszanie błędów HTTP 403 (Dostęp zabroniony), prawdopodobną przyczyną jest powitania klienta używa wygasłe dostępu sygnatury dostępu Współdzielonego podczas wysyłania żądania magazynu (mimo że inne przyczyny obejmują zegara pochylenia nieprawidłowe klucze, a pusty nagłówki). Wygasłe klucza sygnatury dostępu Współdzielonego jest przyczyną hello, nie będą widzieć żadnych wpisów rejestrowania magazynu danych dziennika programu hello po stronie serwera. Witaj poniższej tabeli przedstawiono przykładowe z dziennika klienta hello generowane przez hello biblioteki klienta magazynu, która ilustruje ten problem występuje:

| Element źródłowy | Poziom szczegółowości | Poziom szczegółowości | Identyfikator żądania klienta | Operacja tekstu |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Informacje |3 |85d077ab-... |Uruchamianie operacji z lokalizacji podstawowej na tryb lokalizacji PrimaryOnly. |
| Microsoft.WindowsAzure.Storage |Informacje |3 |85d077ab-... |Uruchamianie synchroniczne żądania toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;si = mypolicy&amp;sig = OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Informacje |3 |85d077ab-... |Oczekiwanie na odpowiedź. |
| Microsoft.WindowsAzure.Storage |Ostrzeżenie |2 |85d077ab-... |Zgłoszono wyjątek podczas oczekiwania na odpowiedź: hello serwer zdalny zwrócił błąd: (403) zabroniony. |
| Microsoft.WindowsAzure.Storage |Informacje |3 |85d077ab-... |Odebrano odpowiedź. Kod stanu = 403, identyfikator żądania = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = ETag =. |
| Microsoft.WindowsAzure.Storage |Ostrzeżenie |2 |85d077ab-... |Zgłoszono wyjątek podczas operacji hello: hello serwer zdalny zwrócił błąd: (403) zabroniony. |
| Microsoft.WindowsAzure.Storage |Informacje |3 |85d077ab-... |Sprawdzanie, czy należy wykonać ponownie operację hello. Liczba ponownych prób = 0, kod stanu HTTP 403, wyjątek = = powitania serwera zdalnego zwróciło błąd: (403) zabroniony. |
| Microsoft.WindowsAzure.Storage |Informacje |3 |85d077ab-... |ustawiono Hello następnej lokalizacji tooPrimary, na podstawie hello trybu lokalizacji. |
| Microsoft.WindowsAzure.Storage |Błąd |1 |85d077ab-... |Zasady ponawiania nie zezwala na ponowienie próby. Niepowodzenie z powitania serwera zdalnego zwróciło błąd: (403) zabroniony. |

W tym scenariuszu należy zbadać, dlaczego tokenu sygnatury dostępu Współdzielonego hello wygasa przed powitania klienta wysyła hello toohello tokenu serwera:

* Zwykle nie należy ustawić czas rozpoczęcia, podczas tworzenia sygnatury dostępu Współdzielonego dla toouse klienta natychmiast. W przypadku małych zegara różnice między hostem hello generowania przy użyciu sygnatury dostępu Współdzielonego hello hello bieżący czas i usługi magazynu hello, a następnie jest możliwe hello magazynu usługi tooreceive sygnatury dostępu Współdzielonego, który nie jest jeszcze ważny.
* Czas wygaśnięcia bardzo krótki nie należy ustawiać na sygnatury dostępu Współdzielonego. Ponownie, małych zegara różnice między hostem hello generowania hello sygnatury dostępu Współdzielonego i usługi magazynu hello może prowadzić tooa SAS najwyraźniej wygasa wcześniej niż zakładano.
* Witaj parametr wersji w hello klucza sygnatury dostępu Współdzielonego (na przykład **sv = 2012-02-12**) wersja hello dopasowania hello korzystasz z biblioteki klienta usługi Storage. Zawsze należy używać najnowszej wersji hello hello biblioteki klienta usługi Storage. Aby uzyskać więcej informacji o wersji tokenu sygnatury dostępu Współdzielonego, zobacz [Nowości dotyczące usługi Magazyn Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/14/what-s-new-for-microsoft-azure-storage-at-teched-2014.aspx).
* * Ponownego generowania kluczy dostępu do magazynu (kliknij **Zarządzaj kluczami dostępu** na każdej stronie na koncie magazynu w hello klasycznego portalu Azure) to unieważnienie wszystkie istniejące tokeny sygnatury dostępu Współdzielonego. Może to być problem, jeśli Generowanie tokeny sygnatury dostępu Współdzielonego i czas wygaśnięcia długi dla toocache aplikacji klienta.

Jeśli używasz hello tokeny sygnatury dostępu Współdzielonego toogenerate biblioteki klienta usługi Storage, a następnie jest toobuild łatwa prawidłowy token. Jednak jeśli jesteś przy użyciu interfejsu API REST magazynu hello i ręcznie konstruowania tokeny sygnatury dostępu Współdzielonego hello należy uważnie przeczytać temat hello <a href="http://msdn.microsoft.com/library/azure/ee395415.aspx" target="_blank">Delegowanie dostępu z sygnaturą dostępu współdzielonego</a> w witrynie MSDN.

### <a name="the-client-is-receiving-404-messages"></a>powitania klienta odbiera komunikaty HTTP 404 (nie znaleziono)
Jeśli aplikacja kliencka hello odbiera komunikat HTTP 404 (nie znaleziono) z serwera hello, oznacza to próbowano powitania klienta hello obiektu toouse (na przykład jednostki, tabeli, obiektów blob, kontenera lub kolejki) nie istnieje w usłudze magazynowania hello. Istnieje wiele możliwych przyczyn tej, takich jak:

* [powitania klienta lub inny proces wcześniej usunięty obiekt hello]
* [Problem autoryzacji dostępu sygnatury dostępu Współdzielonego]
* [Kod JavaScript po stronie klienta nie ma obiektu hello tooaccess uprawnień]
* [Błąd sieci]

#### <a name="client-previously-deleted-the-object"></a>powitania klienta lub inny proces wcześniej usunięty obiekt hello
W scenariuszach, w którym klient hello próbuje tooread, aktualizacji lub usuwania danych w usłudze magazynowania, który zazwyczaj jest to łatwe tooidentify powitania po stronie serwera rejestruje poprzedniej operacji usunięty z usługi magazynowania hello hello danego obiektu. Bardzo często dane dziennika hello pokazuje tego innego obiektu usuniętego hello użytkownika lub inny proces. W dzienniku rejestrowania magazynu po stronie serwera hello hello typ operacji i żądanego obiektu-kolumn klucza pokazują, gdy klient usunięty obiekt.

W scenariuszu hello którym klient próbuje tooinsert obiektu nie można od razu widoczne Dlaczego powoduje to odpowiedzi HTTP 404 (nie znaleziono) biorąc pod uwagę, że hello klienta jest utworzenie nowego obiektu. Jednak jeśli powitania klienta jest utworzenie obiektu blob, który musi być możliwe toofind hello kontenera obiektów blob, powitania klienta jest tworzenia komunikatu musi być możliwe toofind kolejki, a jeśli powitania klienta jest dodawanie wiersza musi być możliwe toofind hello tabeli.

Możesz użyć powitania klienta dziennika z hello toogain biblioteki klienta usługi Storage, które bardziej szczegółowe zrozumienia, gdy powitania klienta wysyła określone żądania toohello magazynu usługi.

Hello następujące dziennika klienta generowane przez biblioteki klienta magazynu hello przedstawiono hello problem podczas powitania klienta nie można odnaleźć kontenera hello dla obiekt blob hello tworzenia. Ten dziennik zawiera szczegóły hello następujące operacje magazynu:

| Identyfikator żądania | Operacja |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** kontenera obiektów blob hello toodelete metody. Należy pamiętać, że ta operacja obejmuje **HEAD** żądania toocheck istnienie hello hello kontenera. |
| e2d06d78... |**CreateIfNotExists** kontenera obiektów blob hello toocreate metody. Należy pamiętać, że ta operacja obejmuje **HEAD** żądania, które sprawdza istnienie hello hello kontenera. Witaj **HEAD** zwraca komunikat 404, ale nadal. |
| de8b1c3c-... |**UploadFromStream** metody toocreate hello blob. Witaj **PUT** żądanie kończy się niepowodzeniem z komunikatem 404 |

Wpisy dziennika:

| Identyfikator żądania | Operacja tekstu |
| --- | --- |
| 07b26a5d-... |Uruchamianie toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer żądań synchronicznych. |
| 07b26a5d-... |StringToSign = HEAD...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 2014 cze 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Oczekiwanie na odpowiedź. |
| 07b26a5d-... |Odebrano odpowiedź. Kod stanu 200, identyfikator żądania = = eeead849... Content-MD5 = ETag = &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Nagłówki odpowiedzi zostały przetworzone pomyślnie, kontynuowanie rest hello hello operacji. |
| 07b26a5d-... |Pobiera treść odpowiedzi. |
| 07b26a5d-... |Operacja została ukończona pomyślnie. |
| 07b26a5d-... |Uruchamianie toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer żądań synchronicznych. |
| 07b26a5d-... |StringToSign = 03 2014 cze DELETE...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Oczekiwanie na odpowiedź. |
| 07b26a5d-... |Odebrano odpowiedź. Kod stanu = 202, identyfikator żądania = 6ab2a4cf..., Content-MD5 = ETag =. |
| 07b26a5d-... |Nagłówki odpowiedzi zostały przetworzone pomyślnie, kontynuowanie rest hello hello operacji. |
| 07b26a5d-... |Pobiera treść odpowiedzi. |
| 07b26a5d-... |Operacja została ukończona pomyślnie. |
| e2d06d78-... |Uruchamianie toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer żądania asynchronicznego.</td> |
| e2d06d78-... |StringToSign = 03 2014 cze HEAD...x-ms-client-request-id:e2d06d78-...x-ms-date:Tue, 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Oczekiwanie na odpowiedź. |
| de8b1c3c-... |Uruchamianie toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt żądań synchronicznych. |
| de8b1c3c-... |StringToSign = PUT... 64.qCmF+TQLPhq/YYK50mP9ZQ==...x-MS-blob-type:BlockBlob.x-MS-Client-Request-ID:de8b1c3c-...x-MS-Date:TUE, 03 2014 cze 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Przygotowywanie danych żądania toowrite. |
| e2d06d78-... |Zgłoszono wyjątek podczas oczekiwania na odpowiedź: hello serwer zdalny zwrócił błąd: (404) nie znaleziono... |
| e2d06d78-... |Odebrano odpowiedź. Kod stanu 404, identyfikator żądania = = 353ae3bc..., Content-MD5 = ETag =. |
| e2d06d78-... |Nagłówki odpowiedzi zostały przetworzone pomyślnie, kontynuowanie rest hello hello operacji. |
| e2d06d78-... |Pobiera treść odpowiedzi. |
| e2d06d78-... |Operacja została ukończona pomyślnie. |
| e2d06d78-... |Uruchamianie toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer żądania asynchronicznego. |
| e2d06d78-... |StringToSign = PUT... 0...x-MS-Client-Request-ID:e2d06d78-...x-MS-Date:TUE, 03 2014 cze 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Oczekiwanie na odpowiedź. |
| de8b1c3c-... |Zapisywanie danych żądania. |
| de8b1c3c-... |Oczekiwanie na odpowiedź. |
| e2d06d78-... |Zgłoszono wyjątek podczas oczekiwania na odpowiedź: hello serwer zdalny zwrócił błąd: konflikt (409). |
| e2d06d78-... |Odebrano odpowiedź. Kod stanu = 409, identyfikator żądania = c27da20e..., Content-MD5 = ETag =. |
| e2d06d78-... |Pobiera treść odpowiedzi błędu. |
| de8b1c3c-... |Zgłoszono wyjątek podczas oczekiwania na odpowiedź: hello serwer zdalny zwrócił błąd: (404) nie znaleziono... |
| de8b1c3c-... |Odebrano odpowiedź. Kod stanu 404, identyfikator żądania = = 0eaeab3e..., Content-MD5 = ETag =. |
| de8b1c3c-... |Zgłoszono wyjątek podczas operacji hello: hello serwer zdalny zwrócił błąd: (404) nie znaleziono... |
| de8b1c3c-... |Zasady ponawiania nie zezwala na ponowienie próby. Niepowodzenie z powitania serwera zdalnego zwróciło błąd: (404) nie znaleziono... |
| e2d06d78-... |Zasady ponawiania nie zezwala na ponowienie próby. Niepowodzenie z powitania serwera zdalnego zwróciło błąd: konflikt (409). |

W tym przykładzie hello dziennik zawiera informacje o powitania klienta jest naprzemiennego wykonywania żądania od hello **CreateIfNotExists** — metoda (żądania identyfikator e2d06d78...) z żądaniami hello z hello **UploadFromStream** (— metoda de8b1c3c...); Zdarza się, ponieważ aplikacja kliencka hello asynchronicznie wywołania tych metod. Należy zmodyfikować kod asynchroniczne hello w powitania klienta tooensure czy tworzy kontener hello przed podjęciem próby wykonania tooupload blob tooa żadnych danych w tym kontenerze. Najlepiej, jeśli należy wcześniej utworzyć wszystkich kontenerów.

#### <a name="SAS-authorization-issue"></a>Problem autoryzacji dostępu sygnatury dostępu Współdzielonego
Jeśli aplikacja kliencka hello prób toouse klucza sygnatury dostępu Współdzielonego, który nie ma niezbędne uprawnienia hello operacji hello, usługa Magazyn hello zwraca klienta toohello komunikat HTTP 404 (nie znaleziono). Na powitania sam czasu, można również wyświetlić wartość niezerową **SASAuthorizationError** w hello metryki.

Hello w poniższej tabeli przedstawiono przykładowy komunikat dziennika po stronie serwera z hello rejestrowania magazynu plików dziennika:

| Nazwa | Wartość |
| --- | --- |
| Czas rozpoczęcia żądania | 2014-05-30T06:17:48.4473697Z |
| Typ operacji     | GetBlobProperties            |
| Stan żądania     | SASAuthorizationError        |
| Kod stanu HTTP   | 404                          |
| Typ uwierzytelniania| Sygnatury dostępu współdzielonego                          |
| Typ usługi       | Obiekt blob                         |
| Adres URL żądania        | https://domemaildist.blob.Core.Windows.NET/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ? sv = 2014-02-14 & sr = c & si = mypolicy & sig = XXXXX&;interfejsu api-version = 2014-02-14 |
| Nagłówka identyfikatora żądania  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| Identyfikator żądania klienta  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |

Należy zbadać, dlaczego aplikacja kliencka próbuje tooperform operacji, który go nie udzielono uprawnienia.

#### <a name="JavaScript-code-does-not-have-permission"></a>Kod JavaScript po stronie klienta nie ma obiektu hello tooaccess uprawnień
Jeśli używasz klienta języka JavaScript i usługi magazynu hello jest zwracania wiadomości HTTP 404, należy sprawdzić następujące błędy JavaScript w przeglądarce hello hello:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> Można użyć narzędzia deweloperskie F12 hello w wiadomości powitania tootrace programu Internet Explorer wymieniane między hello przeglądarki i usługi magazynu hello przy rozwiązywaniu problemów JavaScript po stronie klienta.
> 
> 

Te błędy, ponieważ przeglądarka sieci web hello implementuje hello <a href="http://www.w3.org/Security/wiki/Same_Origin_Policy" target="_blank">zasad samego pochodzenia</a> ograniczenia zabezpieczeń, który uniemożliwia wywołanie interfejsu API w innej domenie na stronie powitania domeny hello strony sieci web jest dostarczany z.

toowork wokół hello JavaScript problem, można skonfigurować między CORS Origin Resource Sharing () dla hello magazynu usługi powitania klienta uzyskuje dostęp do. Aby uzyskać więcej informacji, zobacz <a href="http://msdn.microsoft.com/library/azure/dn535601.aspx" target="_blank">udostępniania zasobów między źródłami (CORS) obsługę usług magazynu Azure</a> w witrynie MSDN.

powitania po przykładowy kod przedstawia sposób tooconfigure Twojego obiektu blob usługi tooallow JavaScript działających w hello tooaccess domeny Contoso obiektu blob w usłudze magazyn obiektów blob:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Błąd sieci
W niektórych sytuacjach pakietów sieciowych utracone może spowodować zwracanie HTTP 404 wiadomości toohello klienta usługi storage toohello. Na przykład, gdy aplikacja kliencka jest usunięcie jednostki z usługi tabel hello widzisz powitania klienta throw raportowania wyjątek magazynu "HTTP 404 (nie znaleziono)" komunikat o stanie z usługi tabeli hello. Podczas badania tabeli hello w usłudze magazynowania tabeli hello Zobacz hello usługi została usunięta jednostki hello zgodnie z żądaniem.

Szczegóły wyjątku powitania klienta hello uwzględnia identyfikatora żądania hello (7e84f12d...) przypisany przez usługę tabeli hello żądania hello: można użyć szczegółów żądania tej informacji toolocate hello w dziennikach magazynu po stronie serwera hello przez wyszukiwanie w hello  **Identyfikator nagłówka żądania** kolumny w pliku dziennika hello. Witaj metryki tooidentify można także używać, gdy awarie, takich jak to wystąpić, a następnie wyszukać hello pliki dziennika w oparciu metryki hello czasu hello rejestrowane tego błędu. Ten przedstawia wpisu dziennika, które hello usunięcia nie powiodła się komunikat o stanie "Client inny błąd HTTP (404)". Hello tego samego wpis dziennika zawiera także identyfikator żądania hello wygenerowanych przez klienta hello w hello **client-request-id** kolumny (813ea74f...).

powitania po stronie serwera dziennika zawiera także innego hasła z hello tego samego **client-request-id** operacji usunięcia wartości (813ea74f...) dla pomyślnego hello tej samej jednostki i z hello sam klienta. Operacja usuwania pomyślne miało miejsce bardzo krótko przed hello żądanie usunięcia nie powiodło się.

Witaj najbardziej prawdopodobną przyczyną tego scenariusza jest powitania klienta wysłała żądanie usunięcia usługi hello jednostki toohello tabeli, które zakończyło się pomyślnie, ale nie otrzymano potwierdzenia z powitania serwera (np. ze względu tooa przejściowego problemu z siecią). powitania klienta następnie automatycznie ponowione hello operacji (przy użyciu hello sam **client-request-id**), a ta ponowna próba nie powiodła się, ponieważ jednostki hello już zostało usunięte.

Jeśli ten problem występuje często, należy zbadać, dlaczego powitania klienta nie powiodło potwierdzeń tooreceive z usługi tabeli hello. Jeśli hello problem jest przerywana, powinien pułapki błąd "HTTP (404) nie została odnaleziona" hello i zaloguj powitania klienta, ale zezwalaj na powitania klienta toocontinue.

### <a name="the-client-is-receiving-409-messages"></a>powitania klienta odbiera komunikaty HTTP 409 (konflikt)
Witaj poniższej tabeli przedstawiono wyodrębniania z hello dziennika po stronie serwera dla dwóch operacji klienta: **DeleteIfExists** a następnie natychmiast przez **CreateIfNotExists** przy użyciu hello tej samej nazwy kontenera obiektów blob. Należy pamiętać, że każda operacja klienta powoduje dwa żądania wysyłane toohello serwera, najpierw **GetContainerProperties** toocheck żądania istnienia kontenera hello, a następnie hello **DeleteContainer** lub  **Tworzony kontener** żądania.

| Znacznik czasu | Operacja | wynik | Nazwa kontenera | Identyfikator żądania klienta |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-... |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-... |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-... |
| 05:10:14.2147723 |Tworzony kontener |409 |mmcont |bc881924-... |

Witaj kodu w aplikacji klienckiej hello usuwa i natychmiast odtwarza kontenera obiektów blob przy użyciu hello samej nazwie: hello **CreateIfNotExists** — metoda (żądań klienta identyfikator bc881924-...) ostatecznie zakończy się niepowodzeniem z hello HTTP 409 (konflikt) Wystąpił błąd. Gdy klient usunie kontenerów obiektów blob, tabel lub kolejek, który znajduje się krótki okres przed nazwa hello znowu dostępne.

powitania klienta aplikacji należy używać nazwy kontenera unikatowy zawsze, gdy tworzy nowe kontenery, jeśli wzorzec Usuń/ponownie utwórz hello jest wspólnej.

### <a name="metrics-show-low-percent-success"></a>Metryki pokazują PercentSuccess niskim lub wpisy dziennika analytics ma operacji ze stanem transakcji ClientOtherErrors
Witaj **PercentSuccess** Metryka przechwytuje procent hello działań, które zostały pomyślnie w oparciu o ich kod stanu HTTP. Operacje z kodów stanu 2XX liczba pomyślnym przeprowadzeniu, podczas gdy operacje z kodów stanu w zakresach 3XX, 4XX i 5XX są liczone jako hello nie powiodło się i dolny **PercentSucess** wartość metryki. W plikach dziennika magazynu po stronie serwera hello, operacje te są rejestrowane ze stanem transakcji **ClientOtherErrors**.

Jest ważne toonote, że te operacje zostały pomyślnie ukończone i w związku z tym nie ma wpływu na inne metryki, np. dostępność. Niektóre operacje, które wykonana pomyślnie, ale który może skutkować niepowodzeniem kody stanu HTTP należą:

* **ResourceNotFound** (nie znaleziono 404), na przykład z GET żądania tooa obiektu blob, który nie istnieje.
* **ResouceAlreadyExists** (409 Konflikt), na przykład z **CreateIfNotExist** operacji, gdy hello zasobów już istnieje.
* **ConditionNotMet** (nie modyfikować 304), na przykład z warunkowego operacji, takich jak kiedy klient wysyła **ETag** wartość i HTTP **If-None-Match** toorequest nagłówka tylko wtedy, gdy obraz od ostatniej operacji hello ma zostały zaktualizowane.

Znajduje się lista często występujące kody błędów interfejsu API REST usług magazynu hello zwracających na stronie powitania <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">często występujące kody błędów interfejsu API REST</a>.

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Metryki pojemności Pokaż nieoczekiwane zwiększenie wykorzystania pojemności magazynu
Jeśli widzisz nagłym, nieoczekiwane wykorzystania pojemności na koncie magazynu można zapoznać się z powodów hello sprawdzając Twoje metryki dostępności; na przykład wzrost hello liczba żądań delete nie powiodło się może prowadzić tooan Zwiększ wysokość hello magazynu obiektów blob, który jest używany jako operacje oczyszczania określonych aplikacji, które użytkownik może mieć oczekiwanych toobe Zwiększ ilość miejsca może nie działać zgodnie z oczekiwaniami (w przypadku przykład ponieważ wygasły tokeny sygnatury dostępu Współdzielonego hello używany dla Zwiększ ilość miejsca).

### <a name="you-are-experiencing-unexpected-reboots"></a>Występują nieoczekiwane ponowne uruchomienie maszyn wirtualnych Azure mających dużej liczby dołączonych dysków VHD
Jeśli maszyna wirtualna Azure (VM) jest duża liczba dołączonych dysków VHD, które znajdują się w hello tego samego konta magazynu może przekroczyć wartości docelowe skalowalności hello konta magazynu powoduje hello toofail maszyny Wirtualnej. Należy sprawdzić hello minuty metryki dla konta magazynu hello (**TotalRequests**/**TotalIngress**/**TotalEgress**) maksymalnej przekracza wartości docelowe skalowalności powitania dla konta magazynu. Witaj w sekcji "[metryki spowodować wzrost PercentThrottlingError]" Aby uzyskać pomoc w określeniu, czy ograniczania wystąpił na koncie magazynu.

Ogólnie rzecz biorąc, każdy poszczególnych danych wejściowych lub wyjściowych operacji na wirtualny dysk twardy z maszyny wirtualnej przekłada zbyt**Get strony** lub **umieścić strony** operacje na powitania bazowy stronicowych obiektów blob. W związku z tym można użyć hello szacowane IOPS dla tootune Twojego środowiska wirtualne dyski twarde ile użytkownik może mieć na koncie magazynu jednego na podstawie hello określone zachowanie aplikacji. Nie zaleca się o więcej niż 40 dysków na koncie magazynu jednego. Zobacz <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">cele dotyczące wydajności i skalowalności magazynu Azure</a> szczegółowe hello bieżącej wartości docelowe skalowalności w przypadku kont magazynu, w szczególności hello całkowita liczba żądań szybkość i całkowitej przepustowości hello typ konta magazynu używasz .
Jeśli doszło do przekroczenia wartości docelowe skalowalności hello konta magazynu, należy umieścić dyski VHD w wielu magazynu innego konta tooreduce hello działania każdego indywidualne konta.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>Problem wynika z przy użyciu emulatora magazynu hello do rozwoju lub testu
Zwykle użyć emulatora magazynu hello podczas tworzenia i testowania tooavoid hello wymagania dotyczące konta magazynu platformy Azure. Witaj typowych problemów, które mogą wystąpić, gdy używasz emulatora magazynu hello są:

* [Funkcja "X" nie działa w emulatorze magazynu hello]
* [Błąd "hello wartość dla jednego z nagłówków hello HTTP nie jest w poprawnym formacie hello" gdy hello przy użyciu emulatora magazynu]
* [Uruchomiony emulator magazynu hello wymaga uprawnień administracyjnych]

#### <a name="feature-X-is-not-working"></a>Funkcja "X" nie działa w emulatorze magazynu hello
emulator magazynu Hello nie obsługuje wszystkich funkcji hello hello usług magazynu Azure, takich jak usługa plików hello. Aby uzyskać więcej informacji, zobacz <a href="http://msdn.microsoft.com/library/azure/gg433135.aspx" target="_blank">różnice między hello emulatora magazynu i usług magazynu Azure</a> w witrynie MSDN.

Dla tych funkcji, które hello magazynu emulatora nie obsługuje, użyj hello usługą magazynu platformy Azure w chmurze hello.

#### <a name="error-HTTP-header-not-correct-format"></a>Błąd "hello wartość dla jednego z nagłówków hello HTTP nie jest w poprawnym formacie hello" gdy hello przy użyciu emulatora magazynu
Podczas testowania aplikacji takich jak używać hello biblioteki klienta usługi Storage przed hello Magazyn lokalny emulatora i metodę wywołania **CreateIfNotExists** niepowodzenia z powodu błędu hello oraz komunikat "hello wartość dla jednego z nagłówków hello HTTP nie jest w Witaj poprawny format." Oznacza to, że hello wersji emulatora magazynu hello używasz nie obsługuje wersji hello biblioteki klienta magazynu hello są używane. Biblioteka klienta usługi Storage Hello dodaje nagłówek hello **x-ms-version** tooall hello żądań ułatwia. Jeśli emulator magazynu hello nie rozpoznaje wartości hello w hello **x-ms-version** nagłówka, odrzuca żądanie hello.

Można użyć powitania klienta biblioteki magazynu dzienniki toosee hello wartość hello **nagłówka x-ms-version** wysyła go. Możesz również sprawdzić wartość hello hello **nagłówka x-ms-version** użycie Fiddler tootrace hello żądań od aplikacji klienta.

W tym scenariuszu zwykle występuje, jeśli podczas instalacji i użycia hello najnowszej wersji biblioteki klienta usługi Storage hello bez aktualizowania hello emulatora magazynu. Należy zainstaluj najnowszą wersję hello emulatora magazynu hello lub Użyj magazynu w chmurze zamiast emulatora hello do projektowania i testowania.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Uruchomiony emulator magazynu hello wymaga uprawnień administracyjnych
Zostanie wyświetlony monit o poświadczenia administratora po uruchomieniu emulatora magazynu hello. Dzieje się tak tylko, gdy emulator magazynu hello hello są inicjowanie po raz pierwszy. Po już zainicjować hello emulatora magazynu, nie trzeba toorun uprawnienia administracyjne go ponownie.

Aby uzyskać więcej informacji, zobacz <a href="http://msdn.microsoft.com/library/azure/gg433132.aspx" target="_blank">zainicjować hello emulatora magazynu przez hello używanie narzędzia wiersza polecenia</a> w witrynie MSDN (można również zainicjować hello emulatora magazynu w programie Visual Studio, który będzie również wymagają uprawnień administratora).

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>Pojawiły się problemy z instalacją hello Azure SDK dla platformy .NET
Podczas próby tooinstall hello SDK kończy się niepowodzeniem w trakcie tooinstall hello emulatora magazynu na komputerze lokalnym. Dziennik instalacji Hello zawiera jedną z następujących wiadomości powitania:

* CAQuietExec: Błąd: tooaccess wystąpienia serwera SQL
* CAQuietExec: Błąd: nie można toocreate bazy danych

Witaj przyczyną jest problem z istniejącej instalacji LocalDB. Domyślnie hello emulator magazynu używa danych toopersist LocalDB, po jego symuluje hello usług magazynu platformy Azure. Uruchamiając hello następujące polecenia w oknie wiersza polecenia przed podjęciem próby hello tooinstall zestawu SDK można zresetować wystąpieniem LocalDB.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Witaj **usunąć** polecenie usuwa stare pliki bazy danych z poprzedniej instalacji hello emulatora magazynu.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Inny problem z usługą magazynu
Jeśli hello poprzedniej sekcje dotyczące rozwiązywania problemów nie zawierają hello problem, który z usługą magazynu, powinna przyjąć hello następujące podejście toodiagnosing i rozwiązywania problemu.

* Określ, czy Twoje metryki toosee zmiany z Twojej oczekiwane zachowanie linii bazowej. Od metryki hello może być stanie toodetermine, czy problem hello jest przejściowy lub stałe i jakie operacje magazynu hello problem ma wpływ na.
* Można użyć informacji metryki hello toohelp wyszukiwania danych dziennika bardziej szczegółowe informacje o błędach występujących po stronie serwera. Te informacje mogą pomóc w rozwiązywania oraz usuwania hello problem.
* Jeśli informacje hello w powitania po stronie serwera nie jest wystarczające problem hello tootroubleshoot pomyślnie, można użyć hello biblioteki klienta usługi Storage dzienników po stronie klienta tooinvestigate hello zachowanie aplikacji klienckiej i narzędzi, takich jak Fiddler, programu Wireshark, i programu Microsoft Message Analyzer tooinvestigate sieci.

Aby uzyskać więcej informacji o używaniu narzędzia Fiddler, zobacz "[dodatku 1: ruchu HTTP i HTTPS toocapture przy użyciu narzędzia Fiddler]."

Aby uzyskać więcej informacji o używaniu programu Wireshark, zobacz "[dodatek 2: ruchu sieciowego przy użyciu programu Wireshark toocapture]."

Aby uzyskać więcej informacji o korzystaniu z programu Microsoft Message Analyzer, zobacz "[dodatku 3: ruchu sieciowego przy użyciu programu Microsoft Message Analyzer toocapture]."

## <a name="appendices"></a>Dodatki
dodatki Hello opisano kilka narzędzi, które mogą być przydatne podczas diagnozowania i rozwiązywania problemów z magazynu Azure (i innych usług). Te narzędzia nie są częścią usługi Azure Storage i niektóre produkty innych firm. W efekcie narzędzia hello omówione w tych dodatki nie są objęte każdej umowy pomocy technicznej, które mogą wiązać Ciebie z Microsoft Azure lub usługi Azure Storage i dlatego jako część procesu oceny należy sprawdzić hello dostępne opcje licencjonowania i pomocy technicznej dostawcy Hello tych narzędzi.

### <a name="appendix-1"></a>Dodatek 1: Przy użyciu narzędzia Fiddler toocapture HTTP i HTTPS ruchu
Fiddler jest przydatne narzędzie do analizy ruchu HTTP i HTTPS hello między aplikacji klienckiej i hello usługą magazynu platformy Azure, którego używasz. Możesz pobrać Fiddler z <a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>.

> [!NOTE]
> Fiddler mogącego zdekodować ruchu HTTPS. należy uważnie przeczytać dokumentacji Fiddler hello toounderstand jak robi to i toounderstand hello zabezpieczenia.
> 
> 

Ten dodatek zawiera krótki przewodnik jak tooconfigure Fiddler toocapture ruchu między hello komputera lokalnego w którym zainstalowano narzędzia Fiddler i hello usług magazynu platformy Azure.

Po uruchomieniu narzędzia Fiddler rozpocznie Przechwytywanie ruchu HTTP i HTTPS na komputerze lokalnym. Witaj Oto niektóre przydatne polecenia sterujące Fiddler:

* Zatrzymaj i uruchom Przechwytywanie ruchu. W menu głównym hello Przejdź zbyt**pliku** , a następnie kliknij przycisk **przechwytywania ruchu** tootoggle Przechwytywanie włączać i wyłączać.
* Zapisz przechwycone dane o ruchu. W menu głównym hello przejść za**pliku**, kliknij przycisk **zapisać**, a następnie kliknij przycisk **wszystkie sesje**: umożliwia toosave hello ruchu w pliku archiwum sesji. Załaduj ponownie archiwum sesji później do analizy lub wysłać żądanie pomocy technicznej tooMicrosoft.

toolimit hello ilość ruchu sieciowego, który przechwytuje Fiddler, możesz użyć filtrów, które są konfigurowane w hello **filtry** hello kartę po zrzut ekranu przedstawia filtr, który przechwytuje tylko ruch wysyłany toohello  **contosoemaildist.TABLE.Core.Windows.NET** końcowego magazynu:

![][5]

### <a name="appendix-2"></a>Dodatku 2: Ruch sieciowy toocapture Wireshark przy użyciu
Wireshark jest analizatora protokołów sieciowych, która umożliwia tooview szczegółowe informacje o pakiecie dla wiele różnych protokołów sieciowych. Możesz pobrać Wireshark z <a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>.

Witaj poniższej procedurze wyjaśniono, jak toocapture szczegółowe informacje pakietu dla ruchu z komputera lokalnego hello zainstalowaną usługą tabeli toohello Wireshark na koncie magazynu Azure.

1. Uruchamianie programu Wireshark na komputerze lokalnym.
2. W hello **Start** sekcji, wybierz hello lokalnego interfejsu sieciowego lub interfejsy, które są połączone toohello internet.
3. Kliknij przycisk **przechwytywania opcje**.
4. Dodaj toohello filtru **filtr przechwytywania** pola tekstowego. Na przykład **hosta contosoemaildist.table.core.windows.net** skonfiguruje Wireshark toocapture tylko pakiety wysyłane tooor z hello punkt końcowy usługi tabel w hello **contosoemaildist** magazynu konto. Aby uzyskać pełną listę filtrów przechwytywania Zobacz <a href="http://wiki.wireshark.org/CaptureFilters" target="_blank">http://wiki.wireshark.org/CaptureFilters</a>.
   
   ![][6]
5. Kliknij przycisk **Start**. Wireshark teraz będzie przechwytywać wszystkie tooor wysyłania pakietów hello z hello punkt końcowy usługi tabel, jak na komputerze lokalnym za pomocą aplikacji klienta.
6. Po zakończeniu, kliknij menu głównego hello **przechwytywania** , a następnie **zatrzymać**.
7. Witaj toosave przechwycone dane w Wireshark przechwytywania pliku, kliknij menu głównego hello **pliku** , a następnie **zapisać**.

WireShark wyróżnione wszelkie błędy, które istnieją w hello **packetlist** okna. Umożliwia także hello **Expert informacji** okna (kliknij **Analizuj**, następnie **Expert informacji**) tooview podsumowanie błędów i ostrzeżeń.

![][7]

Została również wybrana tooview hello TCP danych zgodnie z warstwy aplikacji hello widzi ona hello danych TCP prawym przyciskiem myszy i wybierając **wykonaj strumieniem TCP**. Jest to szczególnie przydatne, jeśli przechwycić z zrzutu bez pliku przechwytywania. Zobacz <a href="http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html" target="_blank">tutaj</a> Aby uzyskać więcej informacji.

![][8]

> [!NOTE]
> Aby uzyskać więcej informacji o korzystaniu z programu Wireshark, zobacz hello <a href="http://www.wireshark.org/docs/wsug_html_chunked/" target="_blank">przewodnik użytkowników programu Wireshark</a>.
> 
> 

### <a name="appendix-3"></a>Dodatku 3: Ruch sieciowy toocapture programu Microsoft Message Analyzer przy użyciu
Możesz użyć programu Microsoft Message Analyzer toocapture HTTP i HTTPS ruchu w podobny sposób tooFiddler i przechwytywania ruchu sieciowego w podobny sposób tooWireshark.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Konfigurowanie śledzenia sesji sieci web przy użyciu programu Microsoft Message Analyzer
tooconfigure sesję śledzenia sieci web dla ruchu HTTP i HTTPS przy użyciu programu Microsoft Message Analyzer, uruchom aplikację Microsoft Message Analyzer hello, a następnie na powitania **pliku** menu, kliknij przycisk **przechwytywania/Trace**. Hello listę scenariuszy śledzenia dostępności, wybierz **serwera Proxy sieci Web**. Następnie w hello **konfiguracji ze scenariusza śledzenia** panelu w hello **HostnameFilter** pole tekstowe, Dodaj hello nazwy punktów końcowych magazynu (można wyszukiwać tych nazwach hello klasycznego portalu Azure). Na przykład jeśli hello jest nazwa konta magazynu Azure **contosodata**, należy dodać następujące toohello hello **HostnameFilter** pole tekstowe:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Znak odstępu oddziela hello nazwy hostów.
> 
> 

Gdy wszystko jest gotowe toostart zbieranie danych śledzenia, kliknij przycisk hello **Start With** przycisku.

Aby uzyskać więcej informacji na temat programu Microsoft Message Analyzer hello **serwera Proxy sieci Web** śledzenia, zobacz <a href="http://technet.microsoft.com/library/jj674814.aspx" target="_blank">dostawcy PEF WebProxy</a> w witrynie TechNet.

wbudowane Hello **serwera Proxy sieci Web** śledzenia w programie Microsoft Message Analyzer jest oparta na Fiddler; można przechwytywać ruch HTTPS po stronie klienta i wyświetlić wiadomości niezaszyfrowane HTTPS. Witaj **serwera Proxy sieci Web** śledzenia działa przez konfigurowanie lokalnego serwera proxy dla całego ruchu HTTP i HTTPS, zapewniająca dostęp toounencrypted wiadomości.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnozowanie problemów z siecią przy użyciu programu Microsoft Message Analyzer
Ponadto toousing hello programu Microsoft Message Analyzer **serwera Proxy sieci Web** szczegóły toocapture śledzenia hello ruchu HTTP/HTTPs między hello aplikacji klienckiej i usługi magazynu hello, można również użyć wbudowanych hello  **Lokalne warstwy łącza** toocapture sieci pakietów informacje śledzenia. Pakietów porzucanych ta umożliwia, takich jak sieci możesz toocapture danych podobne toothat przechwytywania z programu Wireshark i diagnozowanie problemów.

Witaj Poniższy zrzut ekranu przedstawia przykład **lokalnego warstwy łącza** śledzenia z niektórymi **informacyjny** wiadomości powitania **DiagnosisTypes** kolumny. Kliknięcie ikony w hello **DiagnosisTypes** kolumna zawiera szczegóły hello wiadomość hello. W tym przykładzie powitania serwera retransmitowane wiadomości w #305, ponieważ nie otrzymano potwierdzenia z powitania klienta:

![][9]

Utworzenie hello sesji śledzenia programu Microsoft Message Analyzer, można określić filtry tooreduce hello ilość szumu w hello śledzenia. Na powitania **przechwytywania / Trace** służącego do określania śledzenia powitania kliknij na powitania **Konfiguruj** link obok zbyt**Microsoft-Windows-NDIS-PacketCapture**. powitania po zrzut ekranu przedstawia konfigurację filtrujące ruch TCP dla adresów IP hello trzy usług magazynu:

![][10]

Aby uzyskać więcej informacji na temat hello śledzenia Microsoft komunikatów analizatora lokalnego warstwy łącza zobacz <a href="http://technet.microsoft.com/library/jj659264.aspx" target="_blank">dostawcy PEF-NDIS-PacketCapture</a> w witrynie TechNet.

### <a name="appendix-4"></a>Dodatek 4: Przy użyciu danych metryki i dziennika tooview programu Excel
Wiele narzędzi Włącz toodownload hello metryki magazynu danych z magazynu tabel platformy Azure w rozdzielanej formatu, który umożliwia łatwe tooload hello danych do programu Excel dla wyświetlania i analizy. Magazyn rejestrowania danych z magazynu obiektów blob platformy Azure jest już w formacie rozdzielanym, który można załadować do programu Excel. Jednak należy tooadd odpowiednie nagłówki kolumn w hello informacji w oparciu o <a href="http://msdn.microsoft.com/library/azure/hh343259.aspx" target="_blank">Format dziennika analityka magazynu</a> i <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">schemat tabeli metryki analityka magazynu</a>.

tooimport Twojego rejestrowania magazynu danych do programu Excel po go pobrać z magazynu obiektów blob:

* Na powitania **danych** menu, kliknij przycisk **tekst z**.
* Plik dziennika toohello przeglądania tooview i kliknij **importu**.
* W kroku 1 hello **Kreatora importu tekstu**, wybierz pozycję **rozdzielany**.

W kroku 1 hello **Kreatora importu tekstu**, wybierz pozycję **średnik** jako hello tylko ogranicznik i wybierz polecenie podwójnego cudzysłowu jako hello **kwalifikator tekstu**. Następnie kliknij przycisk **Zakończ** i wybierz, gdzie tooplace hello danymi w skoroszycie.

### <a name="appendix-5"></a>Dodatek 5: Monitorowanie za pomocą usługi Application Insights dla programu Visual Studio Team Services
Umożliwia także hello funkcji usługi Application Insights dla programu Visual Studio Team Services jako część wydajności i dostępności monitorowania. To narzędzie można:

* Upewnij się, że usługi sieci web jest dostępna i elastyczny. Czy aplikacja jest witryną sieci web lub aplikacji urządzenia, który używa usługi sieci web, jego test adresu URL co kilka minut z lokalizacji na całym świecie hello i informacją o tym, jeśli występuje problem.
* Szybkie diagnozowanie problemów z wydajnością ani wyjątków w usłudze sieci web. Dowiedz się, jeśli są rozciągnięcia procesora CPU lub innych zasobów, odczytać śladów stosu wyjątków i łatwo wyszukiwać dane dziennika śledzenia. Jeśli hello porzucania wydajności aplikacji poniżej akceptowalnego limity, możemy wysłać wiadomość e-mail. Można monitorować usługi sieci web .NET i Java.

Na powitania momencie pisania usługi Application Insights jest w wersji zapoznawczej. Więcej informacji można znaleźć <a href="http://msdn.microsoft.com/library/azure/dn481095.aspx" target="_blank">usługi Application Insights dla programu Visual Studio Team Services w witrynie MSDN</a>.

<!--Anchors-->
[Wprowadzenie]: #introduction
[Jak jest zorganizowana w tym przewodniku]: #how-this-guide-is-organized

[monitorowania usługi magazynu]: #monitoring-your-storage-service
[Monitorowanie kondycji usługi]: #monitoring-service-health
[Monitorowanie wydajności]: #monitoring-capacity
[Monitorowanie dostępności]: #monitoring-availability
[Monitorowanie wydajności]: #monitoring-performance

[diagnozowanie problemów z magazynowaniem]: #diagnosing-storage-issues
[Problemy z usługi kondycji]: #service-health-issues
[Problemy z wydajnością]: #performance-issues
[Diagnozowanie błędów]: #diagnosing-errors
[Problemy z emulatora magazynu]: #storage-emulator-issues
[Narzędzia rejestrowania magazynu]: #storage-logging-tools
[Przy użyciu narzędzia rejestracji w sieci]: #using-network-logging-tools

[śledzenia End-to-end]: #end-to-end-tracing
[Korelowanie dane dziennika]: #correlating-log-data
[Identyfikator żądania klienta]: #client-request-id
[identyfikator żądania serwera]: #server-request-id
[Znaczniki czasu]: #timestamps

[wskazówki rozwiązywania problemów]: #troubleshooting-guidance
[metryki pokazują AverageE2ELatency wysoki i niski AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Metryki pokazują AverageE2ELatency niski i niski AverageServerLatency, ale występuje duże opóźnienie powitania klienta]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[Metryki wskazują wysoką wartość AverageServerLatency]: #metrics-show-high-AverageServerLatency
[Występują nieoczekiwane opóźnienia w dostarczaniu komunikatów w kolejce]: #you-are-experiencing-unexpected-delays-in-message-delivery

[metryki spowodować wzrost PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Przejściowa wzrost PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Stałe zwiększanie PercentThrottlingError błąd]: #permanent-increase-in-PercentThrottlingError
[metryki spowodować wzrost PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[Metryki wskazują wzrost wartości PercentNetworkError]: #metrics-show-an-increase-in-PercentNetworkError

[powitania klienta odbiera komunikaty HTTP 403 (Dostęp zabroniony)]: #the-client-is-receiving-403-messages
[powitania klienta odbiera komunikaty HTTP 404 (nie znaleziono)]: #the-client-is-receiving-404-messages
[powitania klienta lub inny proces wcześniej usunięty obiekt hello]: #client-previously-deleted-the-object
[Problem autoryzacji dostępu sygnatury dostępu Współdzielonego]: #SAS-authorization-issue
[Kod JavaScript po stronie klienta nie ma obiektu hello tooaccess uprawnień]: #JavaScript-code-does-not-have-permission
[Błąd sieci]: #network-failure
[powitania klienta odbiera komunikaty HTTP 409 (konflikt)]: #the-client-is-receiving-409-messages

[metryki pokazują PercentSuccess niskim lub wpisy dziennika analizy zawierać operacje z Stan transakcji ClientOtherErrors]: #metrics-show-low-percent-success
[Metryki pojemności Pokaż nieoczekiwane zwiększenie wykorzystania pojemności magazynu]: #capacity-metrics-show-an-unexpected-increase
[Występują nieoczekiwane ponowne uruchomienie maszyn wirtualnych, które mają wiele wirtualnych dysków twardych dołączonych]: #you-are-experiencing-unexpected-reboots
[Problem wynika z przy użyciu emulatora magazynu hello do rozwoju lub testu]: #your-issue-arises-from-using-the-storage-emulator
[Funkcja "X" nie działa w emulatorze magazynu hello]: #feature-X-is-not-working
[Błąd "hello wartość dla jednego z nagłówków hello HTTP nie jest w poprawnym formacie hello" gdy hello przy użyciu emulatora magazynu]: #error-HTTP-header-not-correct-format
[Uruchomiony emulator magazynu hello wymaga uprawnień administracyjnych]: #storage-emulator-requires-administrative-privileges
[Pojawiły się problemy z instalacją hello Azure SDK dla platformy .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Inny problem z usługą magazynu]: #you-have-a-different-issue-with-a-storage-service

[dodatki]: #appendices
[dodatku 1: ruchu HTTP i HTTPS toocapture przy użyciu narzędzia Fiddler]: #appendix-1
[dodatek 2: ruchu sieciowego przy użyciu programu Wireshark toocapture]: #appendix-2
[dodatku 3: ruchu sieciowego przy użyciu programu Microsoft Message Analyzer toocapture]: #appendix-3
[Dodatek 4: Przy użyciu danych metryki i dziennika tooview programu Excel]: #appendix-4
[dodatek 5: monitorowanie za pomocą usługi Application Insights dla programu Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/overview.png
[2]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/portal-screenshot.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-2.png
