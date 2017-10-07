---
title: "Lista wydajności i skalowalności magazynu aaaAzure | Dokumentacja firmy Microsoft"
description: "Lista kontrolna sprawdzonych rozwiązań do użycia z usługą Azure Storage w tworzeniu wydajność aplikacji."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c0cd77da4a1abda42c018255ed93215b71f4fad8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Lista kontrolna dotycząca wydajności i skalowalności usługi Microsoft Azure Storage
## <a name="overview"></a>Omówienie
Od czasu wydania hello hello usług Microsoft Azure Storage firma Microsoft opracowała liczba sprawdzonych wskazówki dotyczące korzystania z tych usług w sposób wydajności, i w tym artykule służy tooconsolidate hello najważniejszy je na listę kontrolną stylu. Witaj tego artykułu jest toohelp deweloperzy aplikacji Sprawdź, czy korzystają one z sprawdzonych rozwiązań z usługi Azure Storage i toohelp je zidentyfikować innych sprawdzonych rozwiązań, należy rozważyć stosowanie. W tym artykule nie będzie podejmował toocover co możliwe optymalizacji wydajności i skalowalności —, ale nie uwzględnia te, które są niewielkie ich wpływ lub nie ogólnie dotyczy. toohello jakim hello zachowania aplikacji można przewidzieć podczas projektowania, jest przydatne tookeep w uwadze na wczesnym etapie tooavoid projektów, które będą uruchamiane na problemy z wydajnością.  

Każdy deweloper aplikacji przy użyciu usługi Azure Storage należy podjąć tooread czasu hello w tym artykule i sprawdź, czy aplikacji lub jej zgodny z każdego hello sprawdzonych rozwiązań wymienionych poniżej.  

## <a name="checklist"></a>Lista kontrolna
W tym artykule organizuje hello sprawdzonych rozwiązań w hello następujące grupy. Sprawdzonych rozwiązań mające zastosowanie do:  

* Wszystkie usługi Azure Storage (obiekty BLOB, tabel, kolejek i plików)
* Obiekty blob
* Tabele
* Kolejki  

| Gotowe | Obszar | Kategoria | Zapytania |
| --- | --- | --- | --- |
| &nbsp; | Wszystkie usługi |Wartości docelowe skalowalności |[Tooavoid Twojego aplikacja zbliża się do wartości docelowe skalowalności hello?](#subheading1) |
| &nbsp; | Wszystkie usługi |Wartości docelowe skalowalności |[Jest Twoje nazewnictwa tooenable Konwencji zaprojektowane lepszego równoważenia obciążenia?](#subheading47) |
| &nbsp; | Wszystkie usługi |Sieć |[Czy urządzenia po stronie klienta mają wystarczająco dużej przepustowości i wydajności hello tooachieve małych opóźnieniach potrzebne?](#subheading2) |
| &nbsp; | Wszystkie usługi |Sieć |[Czy urządzenia po stronie klienta mają łącze wystarczająco wysokiej jakości?](#subheading3) |
| &nbsp; | Wszystkie usługi |Sieć |[Aplikacja kliencka hello znajduje się "w pobliżu" hello, konto magazynu?](#subheading4) |
| &nbsp; | Wszystkie usługi |Dystrybucja zawartości |[Używasz CDN do dystrybucji zawartości?](#subheading5) |
| &nbsp; | Wszystkie usługi |Bezpośredni dostęp klienta |[Używasz SAS i mechanizmu CORS toostorage bezpośredni dostęp tooallow zamiast serwera proxy?](#subheading6) |
| &nbsp; | Wszystkie usługi |Buforowanie |[Jest rzadko buforowania danych aplikacji, często używany i zmiany?](#subheading7) |
| &nbsp; | Wszystkie usługi |Buforowanie |[Aplikacja jest przetwarzanie wsadowe aktualizacji (buforowanie je po stronie klienta, a następnie przekazywania w większych zestawów)?](#subheading8) |
| &nbsp; | Wszystkie usługi |Konfiguracja .NET |[Czy skonfigurowano toouse Twojego klienta wystarczającą liczbę równoczesnych połączeń?](#subheading9) |
| &nbsp; | Wszystkie usługi |Konfiguracja .NET |[Czy skonfigurowano toouse .NET wystarczającą liczbę wątków?](#subheading10) |
| &nbsp; | Wszystkie usługi |Konfiguracja .NET |[Używasz .NET 4.5 lub nowszy, która została ulepszona wyrzucanie elementów bezużytecznych?](#subheading11) |
| &nbsp; | Wszystkie usługi |Równoległość |[Ma zapewnić że równoległości jest ograniczone odpowiednio tak, aby nie przeciążać z możliwości klienta albo wartości docelowe skalowalności hello?](#subheading12) |
| &nbsp; | Wszystkie usługi |Narzędzia |[Za pomocą najnowszej wersji programu Microsoft hello podano klienta biblioteki i narzędzia?](#subheading13) |
| &nbsp; | Wszystkie usługi |Ponowne próby |[Czy na pewno przy użyciu wykładniczego wycofywania ponawiania zasady ograniczania błędów i limity czasu?](#subheading14) |
| &nbsp; | Wszystkie usługi |Ponowne próby |[Jest unikanie ponownych prób Twojej aplikacji niepowtarzającego błędów?](#subheading15) |
| &nbsp; | Obiekty blob |Wartości docelowe skalowalności |[Masz dużą liczbę klientów uzyskujących dostęp do pojedynczego obiektu równocześnie?](#subheading46) |
| &nbsp; | Obiekty blob |Wartości docelowe skalowalności |[Aplikacja przebywa w celu hello przepustowości lub operacji skalowalność dla pojedynczego obiektu blob?](#subheading16) |
| &nbsp; | Obiekty blob |Kopiowanie obiektów blob |[Czy kopiowanie blob wydajne?](#subheading17) |
| &nbsp; | Obiekty blob |Kopiowanie obiektów blob |[Używasz narzędzia AzCopy do kopiowania zbiorczego obiektów blob?](#subheading18) |
| &nbsp; | Obiekty blob |Kopiowanie obiektów blob |[Używasz Import/Eksport Azure tootransfer bardzo dużych ilości danych?](#subheading19) |
| &nbsp; | Obiekty blob |Używanie metadanych |[Są przechowywania często używanych metadane dotyczące obiektów blob w ich metadanych?](#subheading20) |
| &nbsp; | Obiekty blob |Przekazywanie Fast |[Podczas próby szybko tooupload jednego obiektu blob, przekazujesz bloki równocześnie?](#subheading21) |
| &nbsp; | Obiekty blob |Przekazywanie Fast |[Podczas próby wiele obiektów blob tooupload szybkie, przekazujesz obiekty BLOB równocześnie?](#subheading22) |
| &nbsp; | Obiekty blob |Popraw typu obiektu Blob |[Używasz stronicowych obiektów blob lub blokowych obiektów blob, gdy jest to potrzebne?](#subheading23) |
| &nbsp; | Tabele |Wartości docelowe skalowalności |[Czy można o hello wartości docelowe skalowalności dla jednostek na sekundę?](#subheading24) |
| &nbsp; | Tabele |Konfiguracja |[Używasz JSON dla żądań tabeli?](#subheading25) |
| &nbsp; | Tabele |Konfiguracja |[Możesz wyłączyć Nagle'a tooimprove hello wydajności małych żądań?](#subheading26) |
| &nbsp; | Tabele |Tabele i partycji |[Ma należy prawidłowo podzielona na partycje danych?](#subheading27) |
| &nbsp; | Tabele |Partycje dynamicznej |[Są jest unikanie tylko Dołącz i tylko dołączy wzorców?](#subheading28) |
| &nbsp; | Tabele |Partycje dynamicznej |[Operacji wstawiania/aktualizacji są rozkładane między wiele partycji?](#subheading29) |
| &nbsp; | Tabele |Zakres kwerendy |[Możesz zaprojektowany z tooallow schematu dla punktu zapytania toobe używane w większości przypadków i używane rzadko toobe zapytania tabeli?](#subheading30) |
| &nbsp; | Tabele |Gęstość zapytania |[Czy skanowania zazwyczaj tylko zapytania i zwracanie wszystkich wierszy, które będą korzystać z aplikacji?](#subheading31) |
| &nbsp; | Tabele |Ograniczenie zwrócone dane |[Używasz filtrowania jednostek zwracająca tooavoid, które nie są potrzebne?](#subheading32) |
| &nbsp; | Tabele |Ograniczenie zwrócone dane |[Używasz tooavoid projekcji zwracanie właściwości, które nie są potrzebne?](#subheading33) |
| &nbsp; | Tabele |Denormalization |[Dane mają nieznormalizowane tak, aby uniknąć nieefektywne zapytania lub wiele żądań odczytu podczas próby tooget danych?](#subheading34) |
| &nbsp; | Tabele |Wstawiania/aktualizowania/usuwania |[Czy partie żądania, które wymagają toobe transakcyjnej lub może odbywać się na powitania sam czas przechodzenia tooreduce?](#subheading35) |
| &nbsp; | Tabele |Wstawiania/aktualizowania/usuwania |[Są możesz uniknąć pobierania toodetermine tylko jednostki czy toocall wstawić lub zaktualizować?](#subheading36) |
| &nbsp; | Tabele |Wstawiania/aktualizowania/usuwania |[Bierzesz pod uwagę przechowywanie serii danych, które często mają zostać pobrane ze sobą w pojedynczej jednostki jako właściwości zamiast wiele jednostek?](#subheading37) |
| &nbsp; | Tabele |Wstawiania/aktualizowania/usuwania |[Dla jednostek, które będą zawsze pobierane ze sobą i mogą być zapisywane w partiach (np. czasu serii danych) bierzesz pod uwagę zamiast tabel za pomocą obiektów blob?](#subheading38) |
| &nbsp; | Kolejki |Wartości docelowe skalowalności |[Czy można o hello wartości docelowe skalowalności komunikatów na sekundę?](#subheading39) |
| &nbsp; | Kolejki |Konfiguracja |[Możesz wyłączyć Nagle'a tooimprove hello wydajności małych żądań?](#subheading40) |
| &nbsp; | Kolejki |Rozmiar komunikatu |[Czy wydajność hello compact tooimprove hello kolejki wiadomości?](#subheading41) |
| &nbsp; | Kolejki |Zbiorcze pobieranie |[Czy pobieranych wiele komunikatów w ramach jednej operacji "Get"?](#subheading42) |
| &nbsp; | Kolejki |Częstotliwość sondowania |[Są sondowania jest często za mało hello tooreduce widocznego opóźnienia aplikacji?](#subheading43) |
| &nbsp; | Kolejki |Komunikat dotyczący aktualizacji |[Używasz UpdateMessage toostore postęp w przetwarzanie komunikatów, co pozwala uniknąć konieczności cała wiadomość hello tooreprocess, jeśli wystąpi błąd?](#subheading44) |
| &nbsp; | Kolejki |Architektura |[Używasz toomake kolejek całej aplikacji skalowalność przechowując obciążeń długotrwałe poza ścieżkę krytyczną hello i skali następnie niezależnie?](#subheading45) |

## <a name="allservices"></a>Wszystkie usługi
Ta sekcja zawiera sprawdzonych rozwiązania, które są odpowiednie toohello używanie tych hello usług Azure Storage (obiekty BLOB, tabel, kolejek lub plików).  

### <a name="subheading1"></a>Wartości docelowe skalowalności
Każda z usług Azure Storage hello ma wartości docelowe skalowalności pojemność (GB), szybkości transakcji i przepustowości. Jeśli aplikacja zbliża się lub przekroczy hello wartości docelowe skalowalności, napotkać opóźnienia zwiększona transakcji lub ograniczenia przepustowości. Gdy usługa Magazyn ogranicza aplikacji, usługa hello rozpoczyna tooreturn "503 Serwer jest zajęty" lub "500 limit czasu operacji" kody błędów dla niektórych transakcji magazynu. W tej sekcji omówiono w szczególności zarówno toodealing ogólne podejście hello z wartości docelowe skalowalności i wartości docelowe skalowalności przepustowości. Kolejnych sekcjach, które zajmują się usługi magazynu omówiono w nim wartości docelowe skalowalności w kontekście hello tej określonej usługi:  

* [Obiekt blob przepustowość i żądań na sekundę](#subheading16)
* [Tabela jednostek na sekundę](#subheading24)
* [Wiadomości w kolejce na sekundę](#subheading39)  

#### <a name="sub1bandwidth"></a>Cel skalowalność przepustowości dla wszystkich usług
W czasie hello zapisu, cele przepustowości hello na koncie hello USA dla magazynu geograficznie nadmiarowego (GRS) są 10 GB/s na sekundę (GB/s) na transfer danych przychodzących (dane przesyłane toohello konta magazynu) i 20 GB/s dla transfer danych wychodzących (dane przesyłane z konta magazynu hello). Konto magazyn lokalnie nadmiarowy (LRS), limity hello są wyższe — 20 GB/s dla przychodzące i 30 GB/s za wyjście.  Limity przepustowości międzynarodowych może być niższa i można znaleźć w naszych [strony elementy docelowe skalowalności](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Aby uzyskać więcej informacji na temat opcji nadmiarowość magazynu hello, zobacz linki hello w [przydatne zasoby](#sub1useful) poniżej.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Jakie toodo, gdy zbliża się docelowy skalowalności
Jeśli aplikacja zbliża się do wartości docelowe skalowalności hello konta pojedynczy magazyn, należy wziąć pod uwagę jedną z następujących podejść hello przyjmowanie:  

* Rozważenia hello obciążeniem, które powoduje, że tooapproach Twojej aplikacji lub przekracza hello skalowalność docelowej. Można zaprojektować go inaczej toouse mniej przepustowości lub pojemności lub mniejszą liczbą transakcji?
* Jeśli aplikacja może przekraczać jedną z wartości docelowe skalowalności hello, należy utworzyć wiele kont magazynu i partycji danych aplikacji w wielu kont magazynu. Jeśli używasz tego wzorca będzie się toodesign aplikacji tak, aby na powitania przyszłych Równoważenie obciążenia sieciowego można dodać więcej kont magazynu. W czasie zapisywania każdej subskrypcji platformy Azure może zawierać maksymalnie too100 kont magazynu.  Konta magazynu ma także żadnego kosztu innych niż użycie pod względem przechowywanych danych, transakcji wykonanych lub przesyłane dane.
* Jeśli aplikacja trafienia hello przepustowości cele, należy wziąć pod uwagę kompresowania dane powitania klienta tooreduce hello przepustowość wymagana toosend hello danych toohello magazynu usługi.  Należy pamiętać, że może to oszczędzić przepustowość i zwiększyć wydajność sieci, mogą mieć jednak również pewne negatywnego wpływu.  Należy ocenić wpływ na wydajność hello tego powodu wymagania dodatkowego przetwarzania toohello kompresji i dekompresji danych powitania klienta. Ponadto przechowywania skompresowane dane można tworzyć bardziej trudnych problemów tootroubleshoot ponieważ może to być trudniejsze danych tooview przechowywane przy użyciu standardowych narzędzi.
* Jeśli aplikacja trafienia hello wartości docelowe skalowalności, upewnij się, że używasz wykładniczego wycofywania ponownych prób (zobacz [ponownych prób](#subheading14)).  Jego lepsze toomake się, że nigdy nie próbują wartości docelowe skalowalności hello (przy użyciu jednego z hello powyżej metody), ale dzięki aplikacji tylko nie będą przechowywać szybkie ponawianie próby, przez co hello ograniczania co gorsza.  

#### <a name="useful-resources"></a>Przydatne zasoby
Witaj następującego łącza zawierają dodatkowe szczegóły na wartości docelowe skalowalności:

* Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) informacji o wartości docelowe skalowalności.
* Zobacz [replikacja usługi Azure Storage](storage-redundancy.md) i hello wpis w blogu [opcje nadmiarowość magazynu Azure i dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) informacji o opcjach nadmiarowość magazynu.
* Aby uzyskać aktualne informacje o cenach dla usług Azure, zobacz [cennik platformy Azure](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Konwencja nazewnictwa partycji
Usługa Azure Storage korzysta z opartej na zakresie partycjonowania schemat tooscale i obciążenia saldo hello systemu. Klucz partycji Hello jest toopartition używane dane do zakresów i tych zakresów są równoważeniem obciążenia na powitania systemu. Oznacza to, że konwencji nazewnictwa, takich jak leksykalne porządkowanie (np. msftpayroll, msftperformance, msftemployees itp.) lub przy użyciu sygnatury czasowe (log20160101, log20160102, log20160102 itp.) będą spowodować w przyszłości zmianę partycje toohello potencjalnie jest kolokowany na powitania tym samym serwerze partycji, dopóki operacja z równoważeniem obciążenia dzieli je na mniejsze zakresów. Na przykład wszystkie obiekty BLOB w kontenerze, mogą być udostępniane przez jeden serwer, dopóki hello obciążenie te obiekty BLOB wymaga dalszych ponowne równoważenie hello partycji zakresów. Podobnie, grupy kont lekkim załadowany z ich nazw, w kolejności leksykalne może być obsługiwana przez pojedynczy serwer do hello obciążenia na jednym lub wszystkie z tych kont wymagają toobe podziału na wielu serwerach partycji. Podczas operacji hello każdej operacji równoważenia obciążenia może mieć wpływ opóźnienia hello wywołań magazynu. toohandle możliwości Hello system, który nagłym serii ruchu tooa partycji jest ograniczona przez hello skalowalność serwera jednej partycji do operacji równoważenia obciążenia hello kopnięć w i rebalances hello zakresem kluczy partycji.  

Można wykonać niektóre najlepszych praktyk tooreduce hello częstotliwość takich operacji.  

* Sprawdź, czy hello konwencji nazewnictwa, używane w przypadku kont, kontenerów, obiektów blob, tabel i kolejek, ściśle. Należy rozważyć prefiksu nazwy kont z 3-cyfrowy skrót przy użyciu funkcji skrótu, który najlepiej odpowiada Twoim potrzebom.  
* Organizowanie danych za pomocą znacznika czasu lub identyfikatory numeryczne, masz tooensure wzorce ruchu tylko Dołącz (lub tylko dołączy) nie jest używany. Te wzorce nie są odpowiednie dla zakresu — na podstawie partycjonowania systemu, i może realizacji tooall hello ruch będzie tooa jednej partycji i ograniczanie system hello z skutecznie równoważenia obciążenia. Na przykład jeśli masz codziennie operacji korzystających z obiektu blob z sygnaturą czasową takich jak RRRRMMDD, następnie cały ruch hello w będący codziennych operacji przekierowanie tooa pojedynczy obiekt, który obsługiwanej przez serwer jednej partycji. Sprawdź czy ogranicza hello na obiekt blob i dla każdej partycji limity potrzeb i Podziel tej operacji w wielu obiektów blob, jeśli to konieczne. Podobnie, jeśli czas serii danych są przechowywane w tabelach, cały ruch hello może być kierowany ostatnia część przestrzeni nazw kluczy hello toohello. Jeśli musisz użyć sygnatury czasowe lub identyfikatory numeryczne, prefiks identyfikatora hello z skrót 3-cyfrowy, lub w przypadku hello sygnatury czasowe prefiks hello część sekund czasu hello, takich jak ssyyyymmdd. Jeśli wykonywane są regularnie wyświetlania i badania operacje, wybierz funkcję wyznaczania wartości skrótu, która powoduje ograniczenie liczby zapytań. W innych przypadkach może być wystarczający losowe prefiks.  
* Aby uzyskać dodatkowe informacje na powitania partycjonowania Schemat używany w usłudze Azure Storage, przeczytaj hello SOSP paper [tutaj](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Sieć
Podczas hello interfejsu API wywołuje sprawy, często ograniczeń sieci fizycznej hello aplikacji hello mieć znaczący wpływ na wydajność. Witaj poniżej opisano niektóre ograniczenia, które użytkownicy mogą wystąpić.  

#### <a name="client-network-capability"></a>Możliwość sieci klienta
##### <a name="subheading2"></a>Przepływność
Przepustowość hello problem jest często możliwości hello powitania klienta. Na przykład, gdy konto magazynu pojedynczego może obsłużyć 10 GB/s lub więcej transfer danych przychodzących (zobacz [wartości docelowe skalowalności przepustowości](#sub1bandwidth)), szybkość sieci hello w wystąpieniu roli procesu roboczego platformy Azure "Małe" obsługuje jedynie około 100 MB/s. Większy wystąpieniach platformy Azure ma kart sieciowych o większej pojemności, więc należy rozważyć użycie większych wystąpienia lub więcej maszyny Wirtualnej, jeśli potrzebujesz wyższe limity sieci z jednego komputera. Jeśli uzyskujesz dostęp do usługi magazynu z aplikacji w lokalnym, a następnie hello zasada dotyczy: zrozumieć funkcje sieci hello powitania klienta urządzenia i toohello łączności sieciowej hello lokalizacji magazynu Azure i albo ich usprawnienia zgodnie z potrzebami lub Projektowanie toowork Twojej aplikacji w ramach ich możliwości.  

##### <a name="subheading3"></a>Jakość łącza
Podobnie jak w przypadku bez użycia sieci należy pamiętać, że warunków sieciowych, co zapewnia błędów i utraty pakietów spowolni skuteczne przepływności.  Za pomocą programu WireShark ani NetMon może pomóc w zdiagnozowaniu tego problemu.  

##### <a name="useful-resources"></a>Przydatne zasoby
Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych i przydzielonej przepustowości, zobacz [rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [rozmiarów maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Lokalizacja
W dowolnym środowisku rozproszonym umieszczenie powitania klienta w pobliżu serwera toohello dostarcza w hello najlepszą wydajność. Do uzyskiwania dostępu do usługi Azure Storage z hello można uzyskać najmniejsze opóźnienia, najlepszym miejscem powitania klienta znajduje się w hello tego samego regionu systemu Azure. Na przykład jeśli masz witryny sieci Web platformy Azure, która używa usługi Azure Storage, powinien oba te zlokalizować w pojedynczym regionie (na przykład nam zachodnie lub Azja południowo-wschodnia). Zmniejsza to opóźnienia hello i hello koszt — w momencie hello zapisu, jest wolne przepustowości w pojedynczym regionie.  

Jeśli w Twojej aplikacji nie znajdują się w obrębie platformy Azure (np. aplikacje urządzenia przenośnego lub lokalne usługi enterprise), następnie ponownie klienta umieszczenie hello konta magazynu w regionie toohello urządzeń, które będą miały dostęp, zazwyczaj zmniejsza opóźnienia. Jeśli klienci szeroko są dystrybuowane (na przykład niektóre w Ameryce Północnej, a niektóre w Europie), a następnie należy rozważyć użycie wielu kont magazynu: jeden znajdujący się w Ameryce Północnej regionu i co Europejskich regionu. Pomoże to opóźnienie tooreduce dla użytkowników w obu regionach. Ta metoda jest zwykle łatwiejsze tooimplement, jeśli hello aplikacji hello magazynów tooindividual określonych użytkowników, a nie wymaga replikowania danych między kontami magazynu.  Do szerokiej dystrybucji zawartości zaleca się CDN — zobacz następną sekcję hello, aby uzyskać więcej informacji.  

### <a name="subheading5"></a>Dystrybucja zawartości
Czasami aplikacji hello tooserve potrzeb tych samych użytkowników toomany zawartości (np. produkt pokaz wideo używane w hello strony głównej witryny sieci Web), znajdujące się w jednym hello tej samej lub w wielu regionach. W tym scenariuszu należy używać dostarczania sieci zawartości (CDN) takie jak usługi Azure CDN, a hello CDN użyje magazynu Azure jako źródła hello hello danych. W przeciwieństwie do konta usługi Azure Storage znajdujące się w pojedynczym regionie, który może dostarczyć zawartość z niskim opóźnieniem tooother regionów usługi Azure CDN używa serwerów w wielu centrach danych wokół hello world. Ponadto CDN zazwyczaj może obsługiwać znacznie wyższe limity wyjście niż konto jednego magazynu.  

Aby uzyskać więcej informacji na temat usługi Azure CDN, zobacz [Azure CDN](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Przy użyciu sygnatury dostępu Współdzielonego i mechanizmu CORS
Jeśli potrzebujesz tooauthorize kodu, takich jak JavaScript w przeglądarce sieci web lub telefon komórkowy dane tooaccess dla aplikacji w usłudze Azure Storage, jednym z podejść jest toouse w roli sieci web jako serwer proxy aplikacji: hello na urządzeniu użytkownika jest uwierzytelniany w usłudze hello roli sieci web, który z kolei uwierzytelnianie przy użyciu usługi magazynu hello. W ten sposób można uniknąć, udostępnianie kluczy konta magazynu na urządzeniach niezabezpieczonych. Jednak ten zostaje umieszczony duże obciążenie na powitania roli sieci web ponieważ wszystkie dane hello przesyłane między urządzeniem użytkownika hello i hello usługi magazynu musi przechodzić przez hello roli sieci web. Możesz uniknąć używania roli sieci web jako serwer proxy dla usług magazynowych hello przy użyciu dostępu sygnatur dostępu Współdzielonego, czasami w połączeniu z nagłówkami współużytkowanie zasobów między źródłami (CORS). Przy użyciu sygnatury dostępu Współdzielonego, można zezwolić na żądania toomake urządzenia użytkownika bezpośrednio tooa magazynu usługi za pomocą tokenu ograniczony dostęp. Na przykład jeśli użytkownik chce tooupload aplikacji tooyour fotografii, roli sieci web można wygenerować i wysłać toohello na urządzeniu użytkownika tokenu sygnatury dostępu Współdzielonego, która udziela konkretnego obiektu blob uprawnień toowrite tooa lub kontener hello dalej 30 minut (po upływie których hello tokenu sygnatury dostępu Współdzielonego wygasa).

Zwykle przeglądarce nie zezwala na JavaScript na stronie hostowanej przez witrynę sieci Web w jednej domenie tooperform określonej operacji, takich jak domeny tooanother "PUT". Na przykład, jeśli na serwerze sieci web rola "contosomarketing.cloudapp.net", a chcesz toouse klienta po stronie JavaScript tooupload konto magazynu obiektów blob tooyour na "contosoproducts.blob.core.windows.net" hello przeglądarki "tego samego źródła policy" zostanie to zabraniać Operacja. CORS to funkcja przeglądarki, która umożliwia hello docelowego (w przypadku konta magazynu wielkość hello) toocommunicate toohello przeglądarki domeny zaufaną żądań pochodzących z domeny źródłowej hello (w tej roli sieci web hello przypadków).  

Oba te technologie mogą pomóc uniknąć niepotrzebnego obciążenia (i wąskich gardeł) w aplikacji sieci web.  

#### <a name="useful-resources"></a>Przydatne zasoby
Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego, zobacz [sygnatury dostępu współdzielonego, część 1: hello opis modelu sygnatur dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md).  

Aby uzyskać więcej informacji na temat CORS, zobacz [udostępniania zasobów między źródłami (CORS) obsługę hello usług magazynu Azure](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Buforowanie
#### <a name="subheading7"></a>Pobieranie danych
Ogólnie rzecz biorąc pobieranie danych z usługą raz jest lepszym rozwiązaniem niż pobierania ich dwa razy. Rozważmy przykład Witaj uruchomiony w roli sieci web, która ma już pobrać obiektu blob 50MB z hello magazynu usługi tooserve jako użytkownik tooa zawartości aplikacji sieci web MVC. aplikacji Hello można następnie pobrać tego samego obiektu blob każdym razem, użytkownik zażąda go lub go można buforować go lokalnie toodisk i ponowne użycie wersja buforowana hello użytkownika kolejnych żądań. Ponadto zawsze, gdy użytkownik zażąda danych hello, hello aplikacji może problem UZYSKAĆ z nagłówkiem warunkowego czas modyfikacji, który będzie uniknąć pobierania hello całego obiektu blob, jeśli nie została zmodyfikowana. Można zastosować ten sam tooworking wzorca z jednostek tabeli.  

W niektórych przypadkach może się okazać, że aplikacja może przyjęto założenie, że tego obiektu blob hello pozostaje ważny przez krótki czas, po pobraniu i że podczas tego okresu hello aplikacji nie jest konieczne toocheck Jeśli zmodyfikowano hello obiektu blob.

Konfiguracja, wyszukiwania i inne dane, które są zawsze używane przez aplikację hello są obiekty doskonale nadające się do buforowania.  

Przykład sposobu tooget hello toodiscover właściwości obiektu blob daty ostatniej modyfikacji przy użyciu platformy .NET, zobacz [zestawu i pobrać właściwości i metadane](storage-properties-metadata.md). Aby uzyskać więcej informacji na temat warunkowego pliki do pobrania, zobacz [warunkowo Odśwież lokalną kopię obiektu Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Przekazywanie danych w partiach
W niektórych scenariuszach aplikacji agregowanie danych lokalnie i następnie okresowo przekaż go w partii, zamiast natychmiast przekazywania każdego elementu danych. Na przykład aplikacja sieci web może przechowywać plik dziennika działań: hello aplikacji można albo przekazać szczegółowe informacje o każdym działaniu zdarza się to jako jednostkę tabeli (co wymaga wielu operacji magazynu), lub można zapisać działania szczegóły tooa lokalnego pliku dziennika, a następnie okresowo Przekaż wszystkie szczegóły działania jako obiekt blob tooa rozdzielonym pliku. W przypadku każdego wpisu dziennika o rozmiarze 1KB rozmiaru, możesz przekazać tysięcy w ramach jednej transakcji "Umieszczanie obiektu Blob" (możesz przekazać obiekt blob z zapasowej too64MB rozmiar w ramach jednej transakcji). Oczywiście jeśli maszyny lokalne powitania awarii przekazywania toohello przed potencjalnie utracisz niektóre dane dziennika: Deweloper aplikacji hello należy projektować pod kątem hello możliwości urządzeń klienckich lub przekazywanie błędów.  Jeśli dane o aktywności hello musi toobe pobierane dla timespans (nie tylko pojedyncze działanie), obiekty BLOB są zalecane przez tabel.

### <a name="net-configuration"></a>Konfiguracja .NET
Jeśli przy użyciu hello .NET Framework, w tej sekcji wymieniono kilka ustawień konfiguracji szybkie służy toomake znaczną poprawę wydajności.  Jeśli używasz innych języków, określ, czy toosee uniwersalne podobne w wybranym języku.  

#### <a name="subheading9"></a>Zwiększenia domyślnego limitu połączenia
W środowisku .NET, hello następującego kodu zwiększa hello domyślnego połączenia limitu (która jest zazwyczaj 2 w środowisku klienta lub 10 w środowisku serwera) too100. Zazwyczaj należy ustawić hello wartość tooapproximately hello liczbę wątków używanych przez aplikację.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Należy ustawić limit połączeń hello przed otwarciem wszystkie połączenia.  

Dla innych języków programowania Zobacz jak ograniczyć połączenia hello tooset toodetermine dokumentacji tego języka.  

Aby uzyskać dodatkowe informacje, zobacz hello blogu [usług sieci Web: równoczesnych połączeń](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>Zwiększ wątków Min puli wątków, jeśli przy użyciu synchronicznej kodu z zadań asynchronicznych
Ten kod spowoduje zwiększenie hello wątków z puli min wątków:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Aby uzyskać więcej informacji, zobacz [metody ThreadPool.SetMinThreads](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Korzystać z platformy .NET 4.5 wyrzucanie elementów bezużytecznych
Użyj .NET 4.5 lub nowszej na powitania klienta aplikacji tootake zaletą ulepszenia wydajności w serwer wyrzucanie elementów bezużytecznych.

Aby uzyskać więcej informacji, zobacz artykuł hello [Omówienie programu poprawy wydajności w programie .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Niepowiązane równoległości
Równoległość mogą być doskonałą wydajność, należy zachować ostrożność przy użyciu danych tooupload lub pobierania niepowiązany równoległości (brak limitu hello liczby wątków i/lub równoległe żądania), za pomocą wielu pracowników tooaccess wiele partycji (kontenerów, kolejki, lub Tabela partycji) w hello tego samego konta magazynu lub tooaccess wielu elementów w hello tej samej partycji. W przypadku niepowiązanego równoległości hello aplikacji można przekracza możliwości urządzeń klienckich hello lub hello wartości docelowe skalowalności konta magazynu co powoduje dłuższe czasy oczekiwania i ograniczania przepustowości.  

### <a name="subheading13"></a>Narzędzia i biblioteki klienta magazynu
Zawsze używaj hello najnowsze firmę Microsoft klienta biblioteki i narzędzia. W czasie hello zapisu są dostępne dla platformy .NET, Windows Phone środowiska wykonawczego systemu Windows, Java i C++ bibliotek klienta, a także biblioteki podglądu dla innych języków. Ponadto firma Microsoft wydała poleceń cmdlet programu PowerShell i polecenia wiersza polecenia platformy Azure do pracy z usługą Azure Storage. Firma Microsoft aktywnie rozwija tych narzędzi z wydajnością na uwadze, jednocześnie dbając o ich zapasowej toodate hello najnowszej wersji usługi i gwarantuje, że obsługują wiele hello wewnętrznie sprawdzonych rozwiązań wydajności.  

### <a name="retries"></a>Ponowne próby
#### <a name="subheading14"></a>Ograniczanie ServerBusy
W niektórych przypadkach usługa Magazyn hello mogą ograniczania aplikacji lub może po prostu być tooserve hello żądania ze względu na stan przejściowy toosome i zwracać komunikat "503 Serwer jest zajęty" lub "500 Timeout".  Może to nastąpić, jeśli aplikacja zbliża się do dowolnej wartości docelowe skalowalności hello lub hello system jest ponowne równoważenie tooallow Twojego partycjonowanej danych umożliwiających uzyskanie większej produktywności.  Aplikacja kliencka Hello zwykle ponów operację hello, powodujący błąd podczas: próba hello same żądania później będzie możliwe. Jednak hello Usługa magazynu jest ograniczania aplikacji, ponieważ jest powyżej wartości docelowe skalowalności lub nawet wtedy, gdy usługa hello było Żądanie hello tooserve innego powodu, agresywne ponownych prób zwykle należy co gorsza problem hello. Z tego powodu należy używać wykładniczej wycofania (powitania klienta biblioteki toothis zachowanie domyślne). Na przykład aplikacja może ponów próbę po 2 sekundy 4 sekundy, a następnie 10 sekund, a następnie 30 sekund, a następnie nadaj całkowicie. Powoduje to zachowanie aplikacji znacznie zmniejszyć jego obciążenie usługi hello zamiast powiększając istniejące problemów.  

Należy pamiętać, że błędy połączenia można ponowić natychmiast, ponieważ nie są hello wyników ograniczania przepustowości i są oczekiwane toobe przejściowej.  

#### <a name="subheading15"></a>Niepowtarzającego — błędy
znane błędy, które mogą ponownych prób, a które nie są są powitania klienta biblioteki. Jednak podczas pisania kodu przed magazynu hello interfejsu API REST, należy pamiętać, występują błędy, które nie powinny ponawiania: na przykład 400 (nieprawidłowe żądanie) odpowiedź wskazuje, tej aplikacji klienckiej hello wysłane żądanie, które nie może być przetworzone, ponieważ jego nie jest w oczekiwanym formularza. Ponowne wysyłanie żądania spowoduje hello sama odpowiedź zawsze, więc nie ma żadnego punktu w ponawianie próby jego. Podczas pisania kodu przed magazynu hello interfejsu API REST, należy pamiętać o jakie błąd hello kodów średnią i hello tooretry właściwy sposób (lub nie) dla każdego z nich.  

#### <a name="useful-resources"></a>Przydatne zasoby
Aby uzyskać więcej informacji o kodach błędów magazynu, zobacz [stanu i kodów błędów](http://msdn.microsoft.com/library/azure/dd179382.aspx) w witrynie sieci web Microsoft Azure hello.  

## <a name="blobs"></a>Obiekty blob
W toohello dodanie sprawdzonych rozwiązań dotyczących [wszystkie usługi](#allservices) opisanych powyżej, zastosuj następujące hello sprawdzonych rozwiązań w szczególności usługa blob toohello.  

### <a name="blob-specific-scalability-targets"></a>Wartości docelowe skalowalności specyficzne dla obiektów blob
#### <a name="subheading46"></a>Wielu klientów jednocześnie dostęp do pojedynczego obiektu
Jeśli masz dużą liczbę klientów uzyskujących dostęp do pojedynczego obiektu jednocześnie należy tooconsider na wartości docelowe skalowalności konta obiekt i magazynu. Hello dokładna liczba klientów, którzy mogą uzyskiwać dostęp do pojedynczego obiektu będą się różnić w zależności od czynników, takich jak liczba hello jednocześnie żądania obiektu hello klientów hello rozmiar obiektu hello, sieci warunki itp.

Jeśli obiekt hello mogą być dystrybuowane za pośrednictwem podawana CDN, taką jak obrazy lub filmy wideo z witryny sieci Web, a następnie należy używać sieci CDN. Zobacz [tutaj](#subheading5).

W innych sytuacjach, takich jak naukowych symulacje przypadku poufnych danych hello dostępne są dwie opcje. Hello jest najpierw toostagger, który Twoje obciążenie dostępu takie hello obiekt jest dostępny w danym okresie czasu vs uzyskiwany jednocześnie. Alternatywnie możesz tymczasowo skopiować hello obiektu toomultiple kont magazynu co pozwala zwiększyć hello całkowita IOPS dla każdego obiektu i wielu kont magazynu. Podczas testowania ograniczone znaleziono, że około 25 maszyn wirtualnych jednocześnie można pobrać obiektu blob 100GB, równoległe (każda maszyna wirtualna została parallelizing hello pobierania za pomocą wątków 32). Jeśli użytkownik ma 100 klientów konieczności tooaccess hello obiektu, najpierw skopiuj go tooa drugiego konta magazynu ma hello najpierw 50 maszyn wirtualnych dostęp hello pierwszego obiektu blob i hello drugi 50 maszyn wirtualnych dostęp hello drugi obiekt blob. Wyniki różni się zależnie od Twoje zachowanie aplikacji, więc należy przetestować, to podczas projektowania. 

#### <a name="subheading16"></a>Przepustowości i operacji na obiektów Blob
Użytkownik może odczytać lub zapisać tooa pojedynczego obiektu blob w górę tooa maksymalnie 60 MB na sekundę (jest to około 480 MB/s przekracza możliwości hello wiele sieci po stronie klienta (w tym hello fizycznej karty Sieciowej na urządzeniu klienckim hello). Ponadto pojedynczego obiektu blob obsługuje too500 żądań na sekundę. Jeśli wielu klientów, którzy potrzebują tooread hello tego samego obiektu blob i może zostać przekroczona te limity, należy rozważyć użycie sieci CDN do dystrybucji hello obiektu blob.  

Aby uzyskać więcej informacji o przepływności docelowej dla obiektów blob, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Kopiowanie i przenoszenie obiektów blob
#### <a name="subheading17"></a>Kopiowanie obiektu Blob
Magazyn Hello interfejsu API REST wersji 2012-02-12 wprowadzone hello przydatne możliwości toocopy blob na kontach: aplikacja kliencka poinstruować hello magazynu usługi toocopy obiektu blob z innego źródła (prawdopodobnie w innego konta magazynu), a następnie umożliwił hello Usługa wykonać kopiowania hello asynchronicznie. To znacznie zmniejszyć przepustowość hello potrzebnych dla aplikacji hello, gdy są migrację danych z innych kont magazynu, ponieważ nie wymagają toodownload i przekazywanie danych hello.  

Pierwsza kwestia, jest jednak, że jeśli kopiowanie odbywa się między kontami magazynu, nie ma żadnej gwarancji czas na podczas kopiowania hello zostanie zakończony. Jeśli aplikacja wymaga obiektu blob szybkie kopiowanie pod kontrolą toocomplete, może być lepiej blob hello toocopy ją pobrać tooa maszyny Wirtualnej, a następnie przekazać go toohello docelowego.  W przypadku pełnego przewidywalności w takiej sytuacji, upewnij się, czy hello kopiowania jest wykonywana przez maszynę Wirtualną w hello tego samego regionu Azure, w przeciwnym razie warunków sieciowych może i prawdopodobnie zostaną mają wpływ na wydajność kopiowania.  Ponadto można monitorować postęp hello asynchroniczne kopii programowo.  

Należy pamiętać, że kopiuje w ramach tego samego konta magazynu się zazwyczaj wykonywane są szybko hello.  

Aby uzyskać więcej informacji, zobacz [kopiowania obiektu Blob](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>Przy użyciu programu AzCopy
Zespół usługi Azure Storage Hello wydała narzędzie wiersza polecenia "AzCopy" oznacza to przeznaczone toohelp z zbiorczego transferu wiele obiektów blob do z i wielu kont magazynu.  To narzędzie jest zoptymalizowana w tym scenariuszu i można osiągnąć dużą szybkością.  Zaleca się jego użycie zbiorczego przekazywanie, pobieranie i scenariuszy kopii. więcej informacji na ten temat toolearn i pobierz go, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Usługa Azure Import/Eksport
Dla bardzo dużych ilości danych (więcej niż 1TB) hello Azure Storage oferuje hello usługi Import/eksport, która umożliwia wysyłanie i pobieranie z magazynu obiektów blob wysyłanie dysków twardych.  Można umieszczać dane na dysku twardym i przesyła tooMicrosoft przekazywania lub wysyłania danych toodownload tooMicrosoft pusty dysk twardy.  Aby uzyskać więcej informacji, zobacz [Użyj hello usługi Import/Eksport Microsoft Azure tooTransfer danych tooBlob magazynu](storage-import-export-service.md).  Może to być znacznie skuteczniejsza niż przekazywanie/pobieranie ten wolumin danych za pośrednictwem sieci hello.  

### <a name="subheading20"></a>Używanie metadanych
Usługa blob Hello obsługuje żądania head, które mogą zawierać metadane dotyczące obiektów blob hello. Na przykład w razie potrzeby aplikacji hello danych EXIF poza zdjęcie go można pobrać zdjęcia hello i wyodrębnij go. toosave przepustowości i zwiększyć wydajność, aplikacja może zapisać danych EXIF hello w metadane obiektu blob hello, gdy aplikacji hello przekazywane zdjęcie hello: można następnie pobrać hello EXIF dane w metadanych za pomocą tylko żądania HEAD, zapisywanie znaczących przepustowości i czas przetwarzania hello wymagane hello tooextract danych EXIF każdy obiekt blob hello czasu jest do odczytu. Powinien to być przydatne w scenariuszach, w którym wystarczy tylko metadane hello i hello pełnej zawartości obiektu blob.  Należy pamiętać, że tylko 8 KB metadane mogą być przechowywane na obiekt blob (hello usługa nie akceptuje toostore żądania większą), więc jeśli danych hello nie mieści się w tym rozmiar, klient nie może być możliwe toouse takie podejście.  

Na przykład jak tooget metadane obiektu blob przy użyciu platformy .NET, zobacz [zestawu i pobrać właściwości i metadane](storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Przekazywanie Fast
blob tooupload jest szybkie, to hello pierwsze pytanie tooanswer: czy przekazywanie obiektu blob jeden lub wiele?  Użyj hello poniżej wskazówki toodetermine hello poprawną metodę toouse w zależności od danego scenariusza.  

#### <a name="subheading21"></a>Szybkie przekazywanie jednego dużych obiektów blob
tooupload pojedynczy dużych obiektów blob szybko, przekazać aplikację kliencką jego bloków lub stron równoległe (co w trosce o wartości docelowe skalowalności hello poszczególne obiekty BLOB i konto magazynu hello jako całość).  Należy zauważyć, że hello oficjalnego bibliotek udostępnionych przez firmę Microsoft klienta RTM magazynu (.NET, Java) toodo możliwości hello to.  Dla każdego z bibliotek hello Użyj hello poniżej poziomu hello tooset określonego obiektu współbieżności:  

* .NET: ParallelOperationThreadCount zestawu na BlobRequestOptions toobe obiekt, używany.
* Java/Android: Użyj BlobRequestOptions.setConcurrentRequestCount()
* Node.js: Użyj parallelOperationThreadCount na obu opcji żądania hello lub hello usługi blob.
* C++: Użyj metody blob_request_options::set_parallelism_factor hello.

#### <a name="subheading22"></a>Szybko przekazać wiele obiektów blob
tooupload wiele obiektów blob szybkie, Przekaż obiekty BLOB równolegle. Jest to szybsza niż przekazywanie jednego obiekty BLOB w czasie z bloku równoległego przekazywania ponieważ rozprzestrzenia się przekazywania hello między wieloma partycjami hello usługi magazynu. Pojedynczego obiektu blob obsługuje tylko przepustowości 60 MB na sekundę (około 480 MB/s). W czasie hello zapisu konto amerykańskiej LRS obsługuje too20 wejściowych GB/s, czyli znacznie większe niż przepustowość hello obsługiwane przez poszczególne obiektu blob.  [Narzędzie AzCopy](#subheading18) wykonuje przekazywanie równoległe domyślnie i jest zalecany dla tego scenariusza.  

### <a name="subheading23"></a>Wybieranie hello poprawnego typu obiektu blob
Usługa Azure Storage obsługuje dwa typy obiektów blob: *strony* obiekty BLOB i *bloku* obiektów blob. Użycie danego scenariusza wybór typu obiektu blob wpłynie na powitania wydajności i skalowalności rozwiązania. Blokowe obiekty BLOB są odpowiednie, można efektywnie tooupload dużych ilości danych: na przykład może być konieczne aplikacji klienckiej zdjęć tooupload lub pamięci masowej tooblob wideo. Stronicowe obiekty BLOB są odpowiednie, jeśli aplikacja hello musi tooperform losowe zapisy na powitania danych: na przykład Azure wirtualne dyski twarde są przechowywane jako stronicowych obiektów blob.  

Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tabele
W toohello dodanie sprawdzonych rozwiązań dotyczących [wszystkie usługi](#allservices) opisanych powyżej, poniżej hello sprawdzonych rozwiązań zastosować w szczególności toohello usługi tabel.  

### <a name="subheading24"></a>Wartości docelowe skalowalności specyficzna dla tabeli
Dodawanie ograniczenia przepustowości toohello całe konto magazynu tabele musi powitania po limit skalowalności określone.  Uwaga hello system będzie równoważenia obciążenia jako Twoje wzrost ruchu, że jeśli seria nagłym ruchu, klient nie może być tooget można od razu tego woluminu przepływności.  Jeśli seria ma deseniu, należy oczekiwać toosee ograniczania przepustowości i/lub przekroczenia limitu czasu podczas hello serii jako usługa Magazyn hello automatycznie równoważy obciążenia, limit tabeli.  Rozwijanie powoli zwykle ma lepsze wyniki jako odpowiednio udostępnia bilans tooload czasu systemu hello.  

#### <a name="entities-per-second-account"></a>Jednostek na sekundę (konto)
limit skalowalności Hello dla uzyskiwania dostępu do tabel działa too20, 000 jednostek (o rozmiarze 1KB każdego) na sekundę dla konta.  Ogólnie rzecz biorąc każdy obiekt, który dodaje się zaktualizowany, usunięty lub skanowania liczby kierunku ten element docelowy.  Dlatego Wstawianie wsadowe, która zawiera 100 jednostek jest traktowane jako 100 jednostek.  Zapytanie, które skanuje 1000 jednostek i zwraca 5 jest traktowane jako 1000 jednostek.  

#### <a name="entities-per-second-partition"></a>Jednostek na sekundę (partycja)
W ramach jednej partycji, hello skalowalność docelowego podczas uzyskiwania dostępu do tabel jest 2000 jednostek (o rozmiarze 1KB każdego) na sekundę, przy użyciu hello tego samego zliczania zgodnie z opisem w poprzedniej sekcji hello.  

### <a name="configuration"></a>Konfiguracja
W tej sekcji przedstawiono kilka ustawień konfiguracyjnych szybki, której można toomake znaczną poprawę wydajności w usłudze tabel hello:  

#### <a name="subheading25"></a>Użyj formatu JSON
Począwszy od wersji usług magazynu 2013-08-15, hello tabeli obsługi usługi za pomocą JSON zamiast hello opartych na języku XML AtomPub format przesyłania danych tabeli. Można zmniejszyć rozmiar ładunku jak 75% i może znacznie poprawić wydajność aplikacji hello.

Aby uzyskać więcej informacji, zobacz hello post [Microsoft Azure tabel: wprowadzenie JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) i [Format ładunku dla operacji usługi tabeli](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Nagle'a wyłączone
Algorytm Nagle'a firmy jest często stosowana w sieciach TCP/IP jako wydajności oznacza tooimprove sieci. Jednak nie jest optymalne we wszystkich okolicznościach (na przykład wysokiej interakcyjne środowiska). Usługi Azure Storage algorytm Nagle'a firmy ma negatywny wpływ na wydajność hello żądań toohello tabeli i kolejki usług i należy go wyłączyć, jeśli to możliwe.  

Aby uzyskać więcej informacji, zobacz nasze wpisie w blogu [nie przyjazną kierunku małych żądań jest algorytm Nagle'a w](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), co wyjaśnia, dlaczego algorytm Nagle'a w słabo współdziała z tabeli i kolejki żądań i przedstawia sposób toodisable go na kliencie aplikacja.  

### <a name="schema"></a>Schemat
Jak reprezentują i wyszukiwanie danych jest hello najważniejszych pojedynczego czynnik, który ma wpływ na wydajność hello hello tabeli usługi. Gdy każda aplikacja jest inny, w tej sekcji opisano niektóre ogólne wskazówki sprawdzonych, które odnoszą się do:  

* Projektowaniu tabel
* Wydajność kwerendy
* Aktualizacje wydajne danych  

#### <a name="subheading27"></a>Tabele i partycji
Tabele są podzielone na partycje. Każdy podmiot przechowywane w partycji udziałów hello sam klucz partycji i ma unikatowy wiersz tooidentify klucza go w ramach tej partycji. Partycje zapewniają korzyści, ale również wprowadzić limity skalowalności.  

* Korzyści: Można aktualizować jednostek hello sam partycji w partii z pojedynczą, atomic, transakcji, która zawiera zapasową too100 przechowywania operacji (limit to łączny rozmiar 4MB). Zakładając, że hello tego samego numeru z toobe jednostek pobrane, możesz także zbadać danych w jednej partycji wydajniej danych obejmującej partycji (mimo że Dowiedz się więcej zaleceń dotyczących przeszukiwaniem danych w tabeli).
* Limit skalowalności: tooentities dostępu przechowywany w jednej partycji nie może być równoważeniem obciążenia ponieważ partycje obsługuje atomic partii transakcji. Z tego powodu hello skalowalność docelowy dla pojedynczej tabeli partycji jest niższa niż hello tabeli usługi jako całość.  

Ze względu na tę charakterystykę tabel i partycje powinna przyjąć hello następujące zasady projektowania:  

* Dane, które aplikacja kliencka często zaktualizowane lub wykonać zapytania w hello tej samej jednostki logicznej pracy powinien znajdować się w hello tej samej partycji.  Może to być, ponieważ aplikacja jest agregowanie zapisy lub ma tootake zaletą operacji wsadowych atomic.  Ponadto danych w jednej partycji mogą być bardziej wydajne wyszukiwane w pojedynczego zapytania niż dane na partycje.
* Dane, które aplikacja kliencka nie wstawiania/aktualizacji lub kwerendy w hello tej samej jednostki logicznej pracy (pojedynczego zapytania lub aktualizację partii) powinien znajdować się w osobnych partycji.  Jeden ważna uwaga jest brak limit nie toohello liczbę kluczy partycji w jednej tabeli, więc o miliony kluczy partycji nie jest problem i nie ma wpływu na wydajność.  Na przykład jeśli aplikacja jest popularnych witryny sieci Web z nazwą logowania użytkownika, przy użyciu identyfikatora użytkownika hello jako klucza partycji hello może być dobrym rozwiązaniem.  

#### <a name="hot-partitions"></a>Partycje dynamicznej
Gorących partycji jest taki, który odbiera nieproporcjonalnie hello ruchu tooan konta, a nie może być o zrównoważonym obciążeniu ponieważ jest on jednej partycji.  Ogólnie rzecz biorąc gorących partycje są tworzone dwa sposoby:  

##### <a name="subheading28"></a>Tylko dołączyć i dołączy tylko wzorce
wzorzec "Dołącz tylko" Hello jest jednym gdzie (większość lub wszystkie) z tooa ruchu hello podane na PK ułatwia i zmniejsza toohello zgodnie z bieżącym czasem.  Przykładem jest Jeśli aplikacja hello bieżącą datę jako klucza partycji dla danych dziennika.  Powoduje to we wszystkich wstawia hello przechodzi toohello ostatniego partycji w tabeli, a hello system nie może załadować saldo, ponieważ wszystkie zapisów hello są będzie toohello koniec tabeli.  Jeśli wolumin hello partycji toothat ruchu przekracza hello skalowalność poziomu partycji docelowej, następnie spowoduje ograniczania.  Jest lepsze tooensure, ruch wysyłany partycje toomultiple hello Równoważenie obciążenia tooenable żądań w tabeli.  

##### <a name="subheading29"></a>Dane o dużym natężeniu ruchu
Jeśli wyniki schemat partycjonowania w jednej partycji zawierającego tylko dane używane znacznie bardziej niż pozostałe partycje, może również zostać wyświetlony ograniczania jako zbliża się do tej partycji docelowej skalowalność hello jednej partycji.  Konieczne jest lepsze toomake się upewnić, że wyniki schemat partycji w pojedynczym nie partycji o wartości docelowe skalowalności hello.  

#### <a name="querying"></a>Wykonywanie zapytania
W tej sekcji opisano sprawdzonych rozwiązań do wykonywania zapytań w usłudze tabel hello.  

##### <a name="subheading30"></a>Zakres kwerendy
Istnieje kilka sposobów toospecify hello zakres tooquery jednostek.  Hello poniżej znajduje się omówienie używa hello każdego z nich.  

Ogólnie rzecz biorąc uniknąć skanowania (większe niż pojedynczy element zapytania), ale jeśli musi przeprowadzić skanowanie, spróbuj tooorganize danych tak, aby Twoje skanowania pobierać dane hello, które wymagają bez skanowania i zwracanie znacznej ilości jednostek, które nie są potrzebne.  

###### <a name="point-queries"></a>Punkt zapytań
Zapytanie punktu pobiera dokładnie jedną jednostkę. Robi to przez określenie zarówno hello klucz partycji i klucz wiersza hello tooretrieve jednostki. Te zapytania są bardzo wydajny i należy ich używać, gdy jest to możliwe.  

###### <a name="partition-queries"></a>Zapytania partycji
Zapytanie partycji jest kwerendę, która pobiera zestawu danych, które współużytkują wspólnego klucza partycji. Zazwyczaj hello zapytanie określa zakres wartości klucza wiersza lub zakres wartości dla niektórych właściwości jednostki w kluczu partycji tooa dodanie. Te są mniej wydajne niż punkt zapytań i powinny być używane rzadko.  

###### <a name="table-queries"></a>Zapytania w tabeli
Zapytanie tabeli jest kwerendę, która pobiera zestaw jednostek, który nie współużytkują wspólnego klucza partycji. Te zapytania nie są wydajne i nie należy ich, jeśli to możliwe.  

##### <a name="subheading31"></a>Gęstość zapytania
Inny kluczowym czynnikiem wydajności zapytania jest hello liczba zwróconych jako liczba porównaniu toohello hello zeskanowane toofind zwróconych ustawione. Jeśli aplikacja wykonuje zapytanie tabeli z filtr dla wartości właściwości, czy tylko 1% udziałów danych hello zapytania hello rozpocznie skanowanie 100 jednostek dla każdej jednostki jeden, zwracana. Hello wartości docelowe skalowalności tabeli omówionych wcześniej wszystkich odnoszą się toohello liczbę jednostek skanowania i nie hello liczba zwróconych: gęstość niski zapytania można łatwo spowodować hello tabeli usługi toothrottle aplikacji ponieważ musi skanować tyle Jednostka hello tooretrieve jednostek, którego szukasz.  Zobacz sekcję hello poniżej na [denormalization](#subheading34) Aby uzyskać więcej informacji na temat tooavoid to.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Ograniczanie hello kwota zwrócone dane
###### <a name="subheading32"></a>Filtrowanie
W przypadku, gdy wiesz, że kwerendy zwróci jednostek, które nie wymagają powitania klienta aplikacji, należy rozważyć użycie hello zwróciła zestaw o rozmiarze hello tooreduce filtru. Jednostek hello nie zwrócony toohello klienta nadal wliczane hello limity skalowalności, wydajność aplikacji będzie poprawy ze względu na rozmiar ładunku sieci hello zmniejszona i hello zmniejszenie liczby jednostek, które musi przetworzyć aplikację kliencką .  Można znaleźć w powyższym Uwaga na [gęstość zapytania](#subheading31), jednak — wartości docelowe skalowalności hello dotyczą toohello liczbę jednostek skanowania, więc zapytania, który odfiltrowuje wiele jednostek może nadal spowodować ograniczania przepustowości, nawet jeśli są zwracane jednostki kilku.  

###### <a name="subheading33"></a>Projekcji
Jeśli aplikacja kliencka musi tylko ograniczony zestaw właściwości z hello jednostek w tabeli, można użyć projekcji toolimit hello rozmiar hello zwrócił zestaw danych. Podobnie jak w przypadku filtrowania, pomaga to tooreduce obciążenia sieci i przetwarzania klienta.  

##### <a name="subheading34"></a>Denormalization
W przeciwieństwie do pracy z relacyjnych baz danych, hello sprawdzonych rozwiązań dotyczących wydajnie przeszukiwaniem danych w tabeli prowadzić toodenormalizing danych. Oznacza to, powielanie hello tych samych danych w wielu jednostkach (jeden dla każdego klucza może używać danych hello toofind) toominimize hello liczbę jednostek zapytania musi zeskanować toofind hello danych powitania klienta potrzeb zamiast dużej liczby jednostek toofind tooscan dane Hello tę aplikację.  Na przykład w witrynie internetowej handlu elektronicznego, możesz toofind kolejności obu według Identyfikatora klienta hello (Udostępnij ten zamówienia) i hello dnia (Udostępnij zamówień w dniu).  W magazynie tabel jest najlepszym jednostki hello toostore (lub tooit odwołania) dwukrotnie — raz z nazwy tabeli, klucz podstawowy i RK znajdowanie toofacilitate według Identyfikatora klienta, raz toofacilitate znalezieniem hello daty.  

#### <a name="insertupdatedelete"></a>Wstawiania/aktualizowania/usuwania
W tej sekcji opisano sprawdzonych rozwiązań jednostek przechowywanych w usłudze tabel hello modyfikowania.  

##### <a name="subheading35"></a>Przetwarzanie wsadowe
Partie transakcji są określane jako jednostki grupy transakcji (ETG) w usłudze Azure Storage; wszystkie operacje hello w ETG muszą należeć do jednej partycji w jednej tabeli. Jeśli to możliwe, należy użyć ETGs tooperform wstawienia, aktualizacje i usunięcia w partiach. To ogranicza hello liczba wystąpień komunikacji dwustronnej z serwerem toohello aplikacji klienta, zmniejsza liczbę hello rozliczeniowy transakcji (ETG traktowana jako pojedynczej transakcji na potrzeby rozliczeń i może zawierać zapasowej too100 operacje magazynu) i umożliwia atomic aktualizacje (wszystkie operacje powiedzie się lub wszystkie się nie powieść w ETG). Środowiska z wysokimi opóźnieniami, takich jak urządzenia przenośne będzie znacznie korzystać z ETGs.  

##### <a name="subheading36"></a>UPSERT
Użyj tabeli **Upsert** operacji tam gdzie to możliwe. Istnieją dwa typy **Upsert**, które może być skuteczniejsza niż tradycyjny **Wstaw** i **aktualizacji** operacje:  

* **InsertOrMerge**: to należy użyć tooupload podzbiór właściwości hello jednostki, ale nie masz pewności, czy jednostka hello już istnieje. Jednostka hello istnieje, to wywołanie aktualizuje właściwości hello zawarte w hello **Upsert** operację i pozostawia wszystkich istniejących właściwości, ponieważ są one, jeśli hello jednostka nie istnieje, wstawia hello nowej jednostki. Jest to podobne toousing rzutowania w zapytaniu, wystarczy tooupload hello właściwości, które zmieniają się.
* **InsertOrReplace**: Użyj go, jeśli chcesz tooupload całkowicie nowe jednostki, ale nie masz pewności, czy już istnieje. Należy używać wyłącznie to po znasz tego hello nowo przekazać jednostki jest całkowicie prawidłowe, ponieważ całkowicie zastępuje hello starego jednostki. Na przykład chcesz tooupdate hello jednostki, która przechowuje bieżącej lokalizacji użytkownika niezależnie od tego, czy aplikacja hello wcześniej przechowywanych danych lokalizacji dla użytkownika hello; nową jednostkę lokalizacji Hello została zakończona i nie są wszystkie informacje z poprzedniego jednostki.

##### <a name="subheading37"></a>Przechowywanie danych serii w pojedynczej jednostki
Czasami aplikacja przechowuje serii danych, że często wymaga ona tooretrieve jednocześnie: na przykład aplikacja może śledzić użycie procesora CPU wraz z upływem czasu, w kolejności tooplot stopniowego wykres danych hello hello ostatnich 24 godzinach. Jednym z podejść jest jednostką jedna tabela toohave na godzinę, z każdej jednostki reprezentującą określoną godzinę i przechowywania hello użycia procesora CPU dla danej godziny. tooplot te dane aplikacji hello musi tooretrieve hello jednostek zawierających dane hello z hello 24 godziny ostatniego.  

Alternatywnie aplikacji można składować użycia hello procesora CPU dla każdej godziny jako osobne właściwość pojedynczej jednostki: tooupdate co godzinę aplikacji można użyć pojedynczego **InsertOrMerge Upsert** wymagają wartości hello tooupdate hello Godzina ostatniej. tooplot hello danych, aplikacja hello musi tylko tooretrieve pojedynczej jednostki zamiast 24, co bardzo wydajny kwerendy (zobacz powyżej dyskusji na [kwerendy zakresu](#subheading30)).

##### <a name="subheading38"></a>Przechowywanie danych strukturalnych w obiektach blob
Czasami strukturalnych danych tak, jak powinien znajdować się w tabelach, ale zakresy jednostek są zawsze pobierane ze sobą i można wstawiać partii.  Dobrym przykładem jest plik dziennika.  W takim przypadku można partii kilka minut dzienników, umieść je i następnie kilka minut dzienników również jednocześnie są zawsze pobierane.  W takim przypadku wydajności, jest lepsze blob toouse zamiast tabel, ponieważ użytkownik można znacznie zmniejszyć liczbę hello obiekty zapisywane/zwrócone, a także zwykle hello liczba żądań, które wymagają wprowadzone.  

## <a name="queues"></a>Kolejki
W toohello dodanie sprawdzonych rozwiązań dotyczących [wszystkie usługi](#allservices) opisanych powyżej, zastosuj następujące hello sprawdzonych rozwiązań w szczególności toohello kolejki usługi.  

### <a name="subheading39"></a>Limity skalowalności
Kolejka może przetworzyć około 2000 wiadomości (1KB) na sekundę (każdego AddMessage, GetMessage i DeleteMessage licznik jako tutaj komunikat). Jeśli to jest niewystarczająca dla aplikacji, należy użyć wielu kolejek i rozmieszczenie do nich wiadomości powitania.  

Wyświetl bieżące wartości docelowe skalowalności w [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md).  

### <a name="subheading40"></a>Nagle'a wyłączone
Zobacz sekcję hello na konfigurację tabeli omówiono algorytm Nagle'a hello — algorytm Nagle'a hello jest zazwyczaj zły hello wydajności kolejki żądań i należy go wyłączyć.  

### <a name="subheading41"></a>Rozmiar komunikatu
Wydajność i skalowalność spadku kolejki miarę zwiększania rozmiaru komunikatu. Tylko hello informacji hello odbiorca musi należy umieścić w wiadomości.  

### <a name="subheading42"></a>Pobieranie partii
Możesz pobrać zapasowych too32 wiadomości z kolejki w ramach jednej operacji. Może to zmniejszyć liczbę hello dwukierunkowe przesyłanie danych z powitania klienta aplikacji, co jest szczególnie przydatne w środowiskach, takich jak urządzenia przenośne, duże opóźnienie.  

### <a name="subheading43"></a>Interwał sondowania kolejki
Większość aplikacji sondować wiadomości z kolejki, która może być jedną z największych źródeł hello transakcji dla tej aplikacji. Wybierz rozsądny sposób interwału sondowania: sondowanie zbyt często może spowodować, że Twoje tooapproach aplikacji hello wartości docelowe skalowalności hello kolejki. Jednak w 200 000 transakcji dla $0,01 (w momencie hello zapisu), przez pojedynczy procesor sondowania, gdy w ciągu sekundy przez miesiąc czy koszt mniej niż 15 centów, więc koszt nie jest zwykle czynnik, który ma wpływ na wybór interwału sondowania.  

Koszt aktualne informacje, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
Można użyć **UpdateMessage** tooincrease hello niewidoczności przekroczenia limitu czasu lub tooupdate informacje o stanie wiadomości. Jest to zaawansowane, należy pamiętać, że każdy **UpdateMessage** operacji liczy się hello skalowalność docelowej. Jednak może to być bardziej efektywnego podejścia niż w przypadku przepływu pracy, który przekazuje zadania z toohello jedna kolejka dalej, ponieważ każdy krok hello zadanie zostało zakończone. Przy użyciu hello **UpdateMessage** operacji umożliwia aplikacji toosave hello zadania stanu toohello wiadomości i kontynuować pracę, zamiast ponownie kolejkowania wiadomości powitania hello kolejny krok opisany hello zadania za każdym razem, gdy wykonuje kroku.  

Aby uzyskać więcej informacji, zobacz artykuł hello [porady: Zmienianie hello zawartość komunikatu w kolejce](storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Architektura aplikacji
Należy użyć toomake kolejek skalowalne architektury aplikacji. Hello poniżej wymieniono niektóre sposoby użycia kolejek toomake skalowalność aplikacji:  

* Można użyć kolejki toocreate zaległości pracy do przetwarzania i wygładzanie obciążeń w aplikacji. Na przykład użytkownik może kolejki żądań od użytkowników tooperform procesora znacznym roboczych takich jak zmiana rozmiaru obrazów przekazane.
* Można użyć kolejek toodecouple części aplikacji, dzięki czemu można je skalować niezależnie. Na przykład frontonu sieci web mógł umieścić wyników ankiety od użytkowników w kolejce dla nowszej analizy i magazynu. Możesz można dodać więcej tooprocess wystąpień roli procesu roboczego hello kolejki danych zgodnie z potrzebami.  

## <a name="conclusion"></a>Podsumowanie
W tym artykule omówiono niektóre hello najbardziej typowych sprawdzonych rozwiązań dla optymalizacji wydajności w przypadku korzystania z usługi Azure Storage. Firma Microsoft zachęca co tooassess Deweloper aplikacji ich stosowania dla każdego hello powyżej rozwiązania i należy wziąć pod uwagę działający na doskonałą wydajność tooget hello zalecenia dotyczące aplikacji korzystających z usługi Azure Storage.
