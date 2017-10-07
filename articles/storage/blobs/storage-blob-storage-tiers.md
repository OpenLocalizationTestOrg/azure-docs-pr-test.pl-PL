---
title: "aaaAzure hot, ostudzić oraz archiwum magazynu obiektów blob | Dokumentacja firmy Microsoft"
description: "Gorący, chłodny i archiwalny magazyn dla kont usługi Azure Blob Storage."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 42fb699bf16147ba8a4d9f75a62debadea5af65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-cool-and-archive-preview-storage-tiers"></a>Azure Blob Storage: warstwa magazynu gorącego, chłodnego i archiwalnego (wersja zapoznawcza)

## <a name="overview"></a>Omówienie

Usługa Azure Storage oferuje trzy warstwy magazynowania dla obiektów blob, co pozwala na najbardziej ekonomiczne przechowywanie danych w zależności od sposobu ich używania. Hello Azure **warstwy magazynu gorącego** jest zoptymalizowana pod kątem przechowywania danych często uzyskuje się dostęp. Hello Azure **warstwy magazynu chłodnego** jest zoptymalizowana pod kątem przechowywania danych, które rzadko uzyskuje dostęp i przechowywane przez co najmniej jeden miesiąc. Witaj [warstwy magazynu archiwum (wersja zapoznawcza)](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) jest zoptymalizowana pod kątem przechowywania danych, które rzadko uzyskuje dostęp i przechowywane przez co najmniej sześć miesięcy wymagania elastyczne czas oczekiwania (w kolejności hello godzin). Witaj *archiwum* warstwy magazynowania można używać tylko na poziomie obiektu blob hello, a nie na koncie magazynu całego hello. Dane w warstwie magazynu chłodnego hello może tolerować nieco niższa dostępność, ale nadal wymagana wysoka trwałość oraz podobny cechy dostępu time i przepływności jako gorących danych. W przypadku chłodnych i archiwalnych danych umowa SLA dotycząca nieco niższej dostępności i wyższe koszty dostępu to dopuszczalne wady, biorąc pod uwagę znacznie niższe koszty magazynowania.

Obecnie dane przechowywane w chmurze hello rośnie w tempie wykładniczym. toomanage koszty dla potrzeb magazynu powiększające, jest przydatne tooorganize danych na podstawie atrybutów, takich jak częstotliwość dostępu i planowanych okresu przechowywania. Dane przechowywane w chmurze hello mogą się różnić pod względem jak jest generowany, przetwarzane i udostępnianych za pośrednictwem swojego okresu istnienia. Do niektórych danych często uzyskuje się dostęp. Są one również często modyfikowane w trakcie całego okresu istnienia. Niektóre dane jest dostępny w okresie użytkowania, często wcześniej z dostęp znacząco jako hello rzadziej. Niektóre dane pozostają nieużywane w chmurze hello i rzadko, jeśli kiedykolwiek, dostęp do raz przechowywane.

W przypadku każdego z tych scenariuszy dostępu do danych istnieją korzyści płynące ze zróżnicowania warstw magazynowania, zoptymalizowanych pod kątem określonego wzorca dostępu. Dzięki warstwom magazynu gorącego, chłodnego i archiwalnego usługa Azure Blob Storage zaspokaja potrzebę korzystania ze zróżnicowanych warstw magazynowania z oddzielnymi modelami cenowymi.

## <a name="blob-storage-accounts"></a>Konta usługi Blob Storage

**Konta usługi Blob Storage** to specjalne konta magazynu służące do przechowywania danych bez struktury jako obiekty blob (obiekty) w usłudze Azure Storage. Z konta magazynu obiektów Blob można teraz wybrać gorąco i warstwy magazynu chłodnego na poziomie konta lub gorąco, cool i archiwizowania warstw na poziomie obiektu blob hello, na podstawie wzorców dostępu. Przechowywania rzadko używanych zimnych danych kosztem hello najniższy magazynu, mniej rzadziej używanych chłodnych danych magazynu niższe koszty niż hot i przechowywać częściej używanych gorących danych hello najniższy koszt dostępu. Konta magazynu obiektów blob są podobne tooyour istniejących kont magazynu ogólnego przeznaczenia i udostępnić wszystkie hello doskonałej trwałości, dostępności, skalowalności i wydajności funkcji używanych dzisiaj, łącznie z 100 procent spójnością interfejsu API dla blokowych obiektów blob i Dołącz obiekty BLOB.

> [!NOTE]
> Konta Magazynu obiektów blob obsługują tylko blokowe obiekty blob i uzupełnialne obiekty blob — stronicowe obiekty blob nie są obsługiwane.

Konta magazynu obiektów blob udostępniają hello **warstwy dostępu** atrybut, który pozwala warstwy magazynowania hello toospecify jako **gorąca** lub **chłodnych** w zależności od hello danych przechowywanych w hello konto. W przypadku zmiany wzorca użycia hello danych, można również przełączać się między tymi warstwami magazynowania, w dowolnym momencie. Hello archiwum warstwy (wersja zapoznawcza) można stosować tylko na poziomie obiektu blob hello.

> [!NOTE]
> Zmiana warstwy magazynowania hello może spowodować naliczenie dodatkowych opłat. Zobacz hello [cenową i rozliczeń](#pricing-and-billing) sekcji, aby uzyskać więcej informacji.

### <a name="hot-access-tier"></a>Warstwa dostępu Gorąca

Przykładowe scenariusze użycia dotyczące warstwy magazynu gorącego hello obejmują:

* Dane, które często uzyskuje się aktywnego użycia lub toobe oczekiwanego dostęp (Odczyt i zapis do).
* Dane, które są przygotowywane do przetwarzania i ewentualnej migracji warstwy magazynu chłodnego toohello.

### <a name="cool-access-tier"></a>Warstwa dostępu Chłodna

Przykładowe scenariusze użycia dotyczące warstwy magazynu chłodnego hello obejmują:

* Krótkoterminowe kopie zapasowe i zestawy danych odzyskiwania po awarii.
* Starszą zawartość nośników nie często wyświetlana, ale jest oczekiwany toobe dostępna natychmiast, gdy dostęp do.
* Duże zbiory danych, które wymagają toobe skutecznie przechowywania koszt celu przyszłego przetwarzania zbierana jest więcej danych. (*np.* długoterminowe magazynowanie danych naukowych lub nieprzetworzonych danych telemetrycznych z zakładu produkcyjnego).

### <a name="archive-access-tier-preview"></a>Warstwa dostępu Archiwalna (wersja zapoznawcza)

[Magazyn archiwum](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) ma hello magazynu najniższy koszt i wyższe toohot kosztów w porównaniu pobierania danych i magazynu chłodnego.

Obiektu blob przechowywanego w magazynie archiwalnym nie można odczytywać, kopiować, zastępować ani modyfikować. Nie można również tworzyć migawek takiego obiektu blob. Może jednak użyć istniejącego toodelete operacje, listy, pobrać metadane właściwości obiektu blob lub zmienić warstwę hello z obiektu blob. tooread dane w archiwum magazynu, należy najpierw zmienić warstwę hello toohot obiektu blob hello lub superpaska. Ten proces jest nazywany Preparaty nawadniające i może potrwać too15 toocomplete godziny dla obiektów blob mniej niż 50 GB. Dodatkowy czas wymagany do większych obiekty BLOB zależy od limit przepływności blob hello.

Zmiana warstwy hello podczas Preparaty nawadniające, można sprawdzić tooconfirm właściwości obiektu blob "archiwum stan" hello. Stan Hello odczytuje "rehydrate oczekujące do gorących" lub "rehydrate oczekujące do chłodnej" w zależności od warstwy docelowej hello. Po zakończenia, hello usunięciu właściwości obiektu blob "archiwum stanu" i "dostępu do warstwy" hello właściwości obiektu blob odzwierciedla hello gorącego i chłodnego warstwy.  

Przykładowe scenariusze użycia dotyczące warstwy magazynu archiwum hello obejmują:

* Długoterminowe kopie zapasowe, dane archiwalne i zestawy danych odzyskiwania po awarii
* Oryginalne (nieprzetworzone) dane, które muszą zostać zachowane, nawet po przetworzeniu ich do ostatecznej użytecznej postaci (*np.* nieprzetworzone pliki multimedialne po transkodowaniu do innych formatów).
* Zgodności i dane archiwalne, wymaga toobe przechowywane przez długi czas, który jest rzadko uzyskuje się dostęp. (*np.* zapisy z kamer monitorujących, stare zdjęcia rentgenowskie lub zdjęcia z rezonansu magnetycznego dla organizacji opieki zdrowotnej, nagrania audio i zapisy rozmów telefonicznych z klientami dla firm z branży usług finansowych).

### <a name="recommendations"></a>Zalecenia

Aby uzyskać więcej informacji dotyczących kont magazynu, zobacz [Informacje o kontach magazynu Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

W przypadku aplikacji wymagających tylko zablokować lub magazynu uzupełnialnych obiektów blob, zaleca się użycie kont magazynu obiektów Blob, tootake zaletą hello zróżnicowane modelu cenowego magazynu warstwowego. Jednak Rozumiemy to mogą nie być możliwe w pewnych okolicznościach gdzie przy użyciu magazynu ogólnego przeznaczenia, który będzie kont hello toogo sposób, takich jak:

* Należy toouse tabel, kolejek lub plików i chcesz, obiektów blob przechowywane w hello tego samego konta magazynu. Należy pamiętać, że nie toostoring żadnych korzyści technicznej w powitalne tego samego konta innego niż mających takie same hello udostępnionych kluczy.

* Nadal potrzebujesz toouse hello klasycznego modelu wdrożenia. Konta magazynu obiektów blob są dostępne tylko za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello.

* Należy toouse stronicowych obiektów blob. Konta Magazynu obiektów blob nie obsługują stronicowych obiektów blob. Ogólnie zaleca się używanie blokowych obiektów blob, chyba że istnieje konkretna potrzeba użycia stronicowych obiektów blob.

* Użyj wersji hello [interfejsu API REST usług Storage](https://msdn.microsoft.com/library/azure/dd894041.aspx) wcześniejsza niż 2014-02-14 lub biblioteka klienta w wersji wcześniejszej niż 4.x i nie można uaktualnić aplikacji.

> [!NOTE]
> Konta usługi Blob Storage są obecnie obsługiwane we wszystkich regionach platformy Azure.
 

## <a name="blob-level-tiering-feature-preview"></a>Funkcja obsługi warstw na poziomie obiektów blob (wersja zapoznawcza)

Obsługa poziomów w poziomie dla obiekt blob umożliwia teraz toochange hello warstwy danych na poziomie obiektu hello przy użyciu jednej operacji o nazwie [ustawić warstwy obiektu Blob](/rest/api/storageservices/set-blob-tier). Można łatwo zmienić hello warstwy dostępu do obiektu blob między hello gorących, chłodnych lub warstw archiwum zmienia wzorce użycia, bez konieczności toomove danych między kontami. Wszystkie zmiany warstw są stosowane natychmiast z wyjątkiem ponownego wypełniania obiektu blob z archiwum. Obiekty BLOB w warstw mogą współistnieć w ramach wszystkich trzech magazynu hello tego samego konta. Żadnych obiektów blob, który nie ma jawnie przypisane warstwy dziedziczy ustawienia warstwy dostępu konta hello hello warstwy.

toouse te funkcje w wersji zapoznawczej, wykonaj te instrukcje hello hello [anonsu blog Azure archiwum i obiektów Blob na poziomie warstwy](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering).

Wykonaj Hello wymieniono niektóre ograniczenia dotyczące wersji zapoznawczej dotyczące tworzenia warstw w poziomie dla obiekt blob:

* Magazyn archiwalny jest obsługiwany tylko dla nowych kont usługi Blob Storage utworzonych w regionie Wschodnie stany USA 2 i pomyślnie zarejestrowanych w wersji zapoznawczej.

* Zarządzanie warstwami na poziomie obiektów blob jest obsługiwane tylko dla nowych kont usługi Blob Storage utworzonych w regionach publicznych i pomyślnie zarejestrowanych w wersji zapoznawczej.

* Magazyn archiwalny i zarządzanie warstwami na poziomie obiektów blob są obsługiwane tylko w przypadku magazynu [LRS] (../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#locally-redundant-storage). [GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#geo-redundant-storage) i [RA-GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#read-access-geo-redundant-storage) będą obsługiwane w przyszłości hello.

* Nie możesz zmienić hello warstwy obiektu blob z migawki.

* Nie można kopiować ani tworzyć migawek obiektu blob przechowywanego w magazynie archiwalnym.

## <a name="comparison-of-hello-storage-tiers"></a>Porównanie warstw magazynowania hello

Witaj w poniższej tabeli przedstawiono porównanie warstw magazynu gorącego i chłodnego hello. Hello archiwum poziom obiektów blob warstwa jest w wersji zapoznawczej, więc nie umowy SLA dla niego.

| | **Warstwa magazynu gorącego** | **Warstwa magazynu chłodnego** |
| ---- | ----- | ----- |
| **Dostępność** | 99,9% | 99% |
| **Dostępność** <br> **(odczyty RA-GRS)**| 99,99% | 99,9% |
| **Opłaty za użycie** | Wyższe koszty magazynowania, niższe koszty dostępu i transakcji | Niższe koszty magazynowania, wyższe koszty dostępu i transakcji |
| **Minimalny rozmiar obiektu** | Nie dotyczy | Nie dotyczy |
| **Minimalny czas magazynowania** | Nie dotyczy | Nie dotyczy |
| **Opóźnienie** <br> **(Czas toofirst bajtu)** | milisekundy | milisekundy |
| **Cele dotyczące skalowalności i wydajności** | Takie same jak w przypadku kont magazynu ogólnego przeznaczenia | Takie same jak w przypadku kont magazynu ogólnego przeznaczenia |

> [!NOTE]
> Magazyn obiektów blob kont hello Obsługa tego samego cele wydajności i skalowalności jako kont magazynu ogólnego przeznaczenia. Aby uzyskać więcej informacji, zobacz [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Cele dotyczące skalowalności i wydajności usługi Magazyn Azure).


## <a name="pricing-and-billing"></a>Cennik i rozliczenia
Konta magazynu obiektów blob, użyj modelu cenowego opartego na powitania warstwy magazynowania. Korzystając z konta magazynu obiektów Blob, zastosuj następujące zagadnienia dotyczące rozliczeń hello:

* **Koszty przechowywania**: oprócz toohello ilości przechowywanych danych hello koszt przechowywania danych różni się w zależności od warstwy magazynowania hello. Hello koszt gigabajt jest niższy dla hello warstwy magazynu chłodnego niż dla warstwy magazynu gorącego hello.

* **Koszty dostępu do danych**: w przypadku danych w warstwie magazynu chłodnego hello są naliczane opłaty za każdy gigabajt danych access odczytów i zapisów.

* **Koszty transakcji**: dla obu warstw istnieje opłata za każdą transakcję. Jednak hello koszt każdej transakcji dla warstwy magazynu chłodnego hello jest wyższa niż w przypadku warstwy magazynu gorącego hello.

* **Koszty transferu danych — replikacja geograficzna**: dotyczy to tylko tooaccounts ze skonfigurowaną replikacją geograficzną, w tym GRS i RA-GRS. Transfer danych w ramach replikacji geograficznej powoduje naliczanie opłaty za każdy gigabajt.

* **Koszty transferu danych wychodzących**: transfery danych wychodzących (dane przesyłane poza region platformy Azure) powodują naliczanie opłat za zużycie przepustowości za każdy gigabajt, co jest spójne z kontami magazynu ogólnego przeznaczenia.

* **Zmiana warstwy magazynowania hello**: Zmiana warstwy magazynu hello z chłodnych toohot wiąże się z tooreading równy opłat wszystkie dane hello istniejących w hello konta magazynu dla każdego przejścia. Na powitania drugiej strony Zmiana warstwy magazynu hello z gorących toocool jest bezpłatna.

> [!NOTE]
> Więcej szczegółów na powitania cennik modelu dla konta magazynu obiektów Blob, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/) strony. Aby uzyskać więcej szczegółów na opłat za transfer danych wychodzących hello, zobacz [szczegóły cennika transferów danych](https://azure.microsoft.com/pricing/details/data-transfers/) strony.

## <a name="quickstart"></a>Szybki start

W tej sekcji przedstawiony hello następujących scenariuszy przy użyciu hello portalu Azure:

* Jak toocreate konta magazynu obiektów Blob.
* Jak toomanage konta magazynu obiektów Blob.

Nie można ustawić tooarchive warstwy dostępu hello w hello następujące przykłady, ponieważ to ustawienie jest stosowane toohello konta całego magazynu. Warstwę archiwalną można ustawić tylko dla określonego obiektu blob.

### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Utwórz konto magazynu obiektów Blob przy użyciu hello portalu Azure

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. W menu Centrum hello wybierz **nowy** > **dane i magazyn** > **konta magazynu**.

3. Wprowadź nazwę konta magazynu.
   
    Ta nazwa musi być globalnie unikatowe; jest on używany jako część adresu URL hello używane obiekty hello tooaccess hello koncie magazynu.  

4. Wybierz **Resource Manager** jako hello modelu wdrażania.
   
    Magazyn warstwowy można używać tylko z kontami magazynu Menedżera zasobów; jest to hello zalecane model wdrażania dla nowych zasobów. Aby uzyskać więcej informacji, zapoznaj się z hello [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).  

5. Z listy rozwijanej Typ konta hello, wybierz **magazynu obiektów Blob**.
   
    Jest to, gdzie wybierz hello typ konta magazynu. Magazyn warstwowy nie jest dostępna w magazynu ogólnego przeznaczenia; jest on dostępny tylko w hello konta typu magazynu obiektów Blob.     
   
    Należy zauważyć, że po wybraniu tej warstwy wydajności hello jest tooStandard. Magazyn warstwowy nie jest dostępny z poziomu wydajności Premium hello.

6. Wybierz opcję replikacji powitania dla konta magazynu hello: **LRS**, **GRS**, lub **RA-GRS**. Domyślnie Hello **RA-GRS**.
   
    Magazyn LRS = magazyn lokalnie nadmiarowy; GRS = magazynu geograficznie nadmiarowego (regiony 2); RA-GRS jest dostęp do odczytu magazynu geograficznie nadmiarowego (2 regionach odczytu access toohello drugi).
   
    Aby uzyskać więcej informacji na temat opcji replikacji usługi Azure Storage, zobacz [Azure Storage replication](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Replikacja usługi Azure Storage).

7. Warstwy magazynowania prawo hello wybierz Twoje potrzeby: hello zestaw **warstwy dostępu** tooeither **chłodnych** lub **gorąca**. Domyślnie Hello **gorąca**. 

8. Wybierz subskrypcję hello, w której ma zostać toocreate hello nowe konto magazynu.

9. Określ nową grupę zasobów lub wybierz istniejącą grupę zasobów. Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

10. Wybierz region hello konta magazynu.

11. Kliknij przycisk **Utwórz** konta magazynu hello toocreate.

### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Zmiana warstwy magazynowania hello konta magazynu obiektów Blob przy użyciu hello portalu Azure

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. toonavigate tooyour konta magazynu, wybierz wszystkie zasoby, a następnie wybierz konto magazynu.

3. W bloku ustawień powitania kliknij **konfiguracji** tooview i/lub zmiana konfiguracji konta hello.

4. Wybierz hello warstwy magazynowania prawo do potrzeb: hello zestaw **warstwy dostępu** tooeither **chłodnych** lub **gorąca**...

5. Kliknij przycisk Zapisz u góry bloku hello hello.

> [!NOTE]
> Zmiana warstwy magazynowania hello może spowodować naliczenie dodatkowych opłat. Zobacz hello [cennik i rozliczenia](#pricing-and-billing) sekcji, aby uzyskać więcej informacji.


## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>Ocenianie i Migrowanie kont magazynu tooBlob
Witaj w tej sekcji służy toohelp użytkowników toomake sprawne przejście kont magazynu obiektów Blob toousing. Istnieją dwa scenariusze dotyczące użytkowników:

* Masz istniejące konto magazynu ogólnego przeznaczenia i chcesz tooevaluate tooa zmiany konta magazynu obiektów Blob z warstwą przechowywania hello.
* Zdecydował toouse konta magazynu obiektów Blob lub już istnieje i ma tooevaluate, czy należy używać warstwy magazynu gorącego i chłodnego hello.

W obu przypadkach hello pierwszej kolejności of business jest tooestimate hello koszt przechowywania i uzyskiwania dostępu do danych przechowywanych na koncie magazynu obiektów Blob i który porównać bieżące koszty.

## <a name="evaluating-blob-storage-account-tiers"></a>Ocenianie warstw dla konta usługi Blob Storage

Kolejność tooestimate hello kosztów przechowywania i uzyskiwania dostępu do danych przechowywanych na koncie magazynu obiektów Blob należy tooevaluate istniejącego wzorca użycia lub przybliżona deseniu oczekiwane wykorzystanie. Ogólnie rzecz biorąc które mają tooknow:

* Wykorzystanie magazynu — jaka ilość danych jest magazynowana i jak ta ilość zmienia się w ciągu miesiąca?

* Z magazynu wzorca dostępu — ilość danych są odczytu z i zapisywane toohello konta (w tym nowych danych)? Ile transakcji jest przeprowadzanych w celu uzyskania dostępu do danych i jakiego rodzaju są to transakcje?

## <a name="monitoring-existing-storage-accounts"></a>Monitorowanie istniejących kont magazynu

toomonitor istniejący magazyn kont i zebrać dane, możesz wprowadzić użycie analityka magazynu Azure, która wykonuje rejestrowanie oraz udostępnia danych metryki dla konta magazynu. Analityka magazynu można przechowywać metryki, które obejmują statystyk i pojemności dane zagregowane transakcji o toohello żądań usługi magazynu obiektów Blob dla obydwu kont magazynu ogólnego przeznaczenia, a także konta magazynu obiektów Blob. Dane te są przechowywane w tabelach dobrze znane w hello tego samego konta magazynu.

Aby uzyskać więcej szczegółowych informacji, zobacz artykuły [About Storage Analytics Metrics (Metryki w usłudze Storage Analytics)](https://msdn.microsoft.com/library/azure/hh343258.aspx) i [Storage Analytics Metrics Table Schema (Schemat tabeli metryk usługi Storage Analytics)](https://msdn.microsoft.com/library/azure/hh343264.aspx).

> [!NOTE]
> Konta magazynu obiektów blob udostępniają punkt końcowy usługi tabel hello tylko do przechowywania i uzyskiwania dostępu do danych metryki powitania dla tego konta.

toomonitor zużycie pamięci masowej hello hello usługi magazynu obiektów Blob, należy metryki pojemności hello tooenable.
Z tym włączone, danych wydajności jest codziennie zarejestrowane dla konta magazynu obiektów Blob usługi i zarejestrowana jako spisu, który jest zapisany toohello *$MetricsCapacityBlob* tabeli w ramach hello same konta magazynu.

wzorca dostępu do danych hello toomonitor dla hello usługi magazynu obiektów Blob, należy tooenable hello co godzinę transakcji metryki na poziomie interfejsu API. Z tym włączone dla interfejsu API transakcji są agregowane co godzinę i rejestrowane jako spisu, który jest zapisany toohello *$MetricsHourPrimaryTransactionsBlob* tabeli w ramach hello same konta magazynu. Witaj *$MetricsHourSecondaryTransactionsBlob* rekordy tabeli hello dodatkowej punktu końcowego toohello transakcji, korzystając z konta magazynu RA-GRS.

> [!NOTE]
> Jeśli masz konto magazynu ogólnego przeznaczenia, w którym są przechowywane stronicowe obiekty blob i dyski maszyny wirtualnej (obok blokowych obiektów blob i danych uzupełnialnych obiektów blob), ten proces szacowania nie ma zastosowania. Jest tak, ponieważ nie ma możliwości odróżnienie pojemności i transakcji metryki na podstawie hello typu obiektu blob dla tylko blokować i uzupełnialnych obiektów blob, które mogą być migrowane tooa konta magazynu obiektów Blob.

tooget dobrej zbliżenia wzorca dostępu i użycia danych, zaleca się wybrać okres przechowywania dla metryki hello jest reprezentatywna regularne użycie i ekstrapolacja. Jedną z opcji jest tooretain hello metryki danych 7 dni i hello zbieranie danych, co tydzień, analizy na końcu hello hello miesiąca. Inną opcją jest dane metryk hello tooretain hello ostatnich 30 dni i zbieranie i analizowanie danych hello na końcu hello hello 30-dniowego okresu.

Aby uzyskać szczegółowe informacje na temat włączania, gromadzenia i wyświetlania danych metryk, zobacz temat [Enabling Azure Storage metrics and viewing metrics data (Włączanie metryk usługi Azure Storage i wyświetlanie danych metryk)](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

> [!NOTE]
> Za przechowywanie i pobieranie danych analitycznych oraz uzyskiwanie dostępu do nich również są naliczane opłaty, podobnie jak za zwykłe dane użytkowników.

### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Przy użyciu kosztów tooestimate metryk użycia

### <a name="storage-costs"></a>Koszty magazynowania

Witaj najnowsze wpisu w tabeli metryki pojemności hello *$MetricsCapacityBlob* kluczem wiersza hello *"dane"* pokazuje hello pojemność magazynu używane przez dane użytkownika. Witaj najnowsze wpisu w tabeli metryki pojemności hello *$MetricsCapacityBlob* kluczem wiersza hello *"analytics"* pokazuje hello pojemność magazynu używane przez hello analizy dzienników.

Następnie można ten całkowita pojemność używane przez oba dzienniki danych i ich analiza użytkownika (jeśli jest włączona) używane tooestimate hello koszt przechowywania danych na koncie magazynu hello. Witaj, tę samą metodę można również podczas szacowania kosztów magazynowania dla blokowych i uzupełnialnych obiektów blob na kontach magazynu ogólnego przeznaczenia.

### <a name="transaction-costs"></a>Koszty transakcji

Suma Hello *"TotalBillableRequests"*, wszystkie pozycje dla interfejsu API w transakcji hello metryki tabela wskazuje hello całkowita liczba transakcji dla tego konkretnego interfejsu API. *Na przykład*, hello łączna liczba *"GetBlob"* transakcji w danym okresie, może zostać obliczona przez hello sumę całkowita liczba żądań rozliczeń dla wszystkich wpisów z kluczem wiersza hello *"użytkownika. GetBlob "*.

Kolejność tooestimate kosztów transakcji dla kont magazynu obiektów Blob należy toobreak dół transakcji hello na trzy grupy ponieważ inaczej cenowo.

* Transakcje zapisu, takie jak *„PutBlob”*, *„PutBlock”*, *„PutBlockList”*, *„AppendBlock"*, *„ListBlobs”*, *„ListContainers”*, *„CreateContainer”*, *„SnapshotBlob”* i *„CopyBlob”*.
* Transakcje usuwania, takie jak *„DeleteBlob”* i *„DeleteContainer”*.
* Wszystkie inne transakcje.

Kolejność tooestimate kosztów transakcji dla kont magazynu ogólnego przeznaczenia należy tooaggregate wszystkich transakcji niezależnie od operacji hello/interfejsu API.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Dostęp do danych i koszty transferu danych replikacji geograficznej

Podczas analizy magazynu nie zapewnia odczytywać hello ilość danych i zapisywane tooa konta magazynu, jego można około oszacować, analizując hello transakcji metryki tabeli. Suma Hello *"TotalIngress"* wszystkie pozycje dla interfejsu API w metryki transakcji hello tabela wskazuje hello łączna ilość danych wejściowych w bajtach dla tego konkretnego interfejsu API. Podobnie hello sumę *"TotalEgress"* wskazuje hello łączna ilość danych wyjściowych, w bajtach.

W kolejności tooestimate hello danych koszty dostępu dla konta magazynu obiektów Blob należy toobreak dół transakcji hello na dwie grupy. 

* Witaj ilość danych pobieranych z konta magazynu hello można oszacować, analizując hello sumę *"TotalEgress"* dla głównie hello *"GetBlob"* i *"CopyBlob"* operacje.

* ilość Hello zapisanych toohello konta magazynu danych można oszacować, analizując hello sumę *"TotalIngress"* dla głównie hello *"Metody PutBlob"*, *"PutBlock"*, *"CopyBlob"* i *"AppendBlock"* operacji.

Koszt Hello transfer danych — replikacja geograficzna dla konta magazynu można obliczyć za pomocą szacowania hello hello ilość danych zapisane po przy użyciu konta magazynu GRS lub RA-GRS obiektu Blob.

> [!NOTE]
> Na przykład bardziej szczegółowych, dotyczących obliczania kosztów hello za pomocą warstwy magazynu gorącego i chłodnego hello, Przyjrzyjmy się hello często Zadawanych pytań *"co to jest aktywny i chłodnej warstw dostępu i jak należy ustalić które jeden toouse?"* w hello [stronie cennika usługi Magazyn Azure](https://azure.microsoft.com/pricing/details/storage/).
 
## <a name="migrating-existing-data"></a>Migrowanie istniejących danych

Konto usługi Blob Storage jest przeznaczone do przechowywania tylko blokowych obiektów blob i uzupełnialnych obiektów blob. Istniejących kont magazynu ogólnego przeznaczenia, które umożliwią toostore tabel, kolejek, plików i dyski, a także obiekty BLOB, nie może być przekonwertowany tooBlob kont magazynu. toouse hello warstw magazynowania, należy toocreate nowego konta magazynu obiektów Blob i przeprowadzić migrację istniejących danych do hello nowo utworzonego konta.

Program hello po metody toomigrate istniejących danych do konta magazynu obiektów Blob z lokalnych urządzeń magazynujących, od dostawców magazynu w chmurze innych firm lub z istniejących kont magazynu ogólnego przeznaczenia na platformie Azure:

### <a name="azcopy"></a>Narzędzie AzCopy

Narzędzie AzCopy to narzędzie wiersza polecenia systemu Windows przeznaczony dla wysokowydajnej kopiowanie tooand danych z usługi Magazyn Azure. Można użyć narzędzia AzCopy toocopy dane na koncie magazynu obiektów Blob z istniejących kont magazynu ogólnego przeznaczenia lub tooupload z lokalnych urządzeń magazynujących na koncie magazynu obiektów Blob.

Aby uzyskać więcej informacji, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Biblioteka przenoszenia danych

Biblioteka przenoszenia danych magazynu Azure dla platformy .NET jest oparta na powitania podstawowym środowisku przenoszenia danych którym działa narzędzie AzCopy. Biblioteka Hello zaprojektowano pod kątem wysokiej wydajności, niezawodnych, i podobne tooAzCopy operacji transferu danych łatwe. Dzięki temu tootake pełne korzyści hello funkcje oferowane przez narzędzie AzCopy w aplikacji natywnie bez konieczności toodeal uruchamiania i monitorowania zewnętrznych wystąpień narzędzia AzCopy.

Aby uzyskać więcej informacji, zobacz [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement) (Biblioteka przenoszenia danych usługi Magazyn Azure dla platformy .NET).

### <a name="rest-api-or-client-library"></a>Interfejs API REST lub biblioteka klienta

Możesz utworzyć toomigrate aplikacji niestandardowych danych do konta magazynu obiektów Blob przy użyciu jednej z bibliotek klienta platformy Azure hello lub hello interfejs API REST usług magazynu Azure. Usługa Azure Storage udostępnia rozbudowane biblioteki dla wielu języków programowania i platform, takich jak .NET, Java, C++, Node.JS, PHP, Ruby i Python. Witaj biblioteki klienta oferują zaawansowane możliwości, takie jak logika ponowień, rejestrowanie i przekazywanie równoległe. Możesz również utworzyć bezpośrednio przed hello interfejsu API REST, które można wywołać za pomocą dowolnego języka, który sprawia, że żądania HTTP i HTTPS.

Aby uzyskać więcej szczegółów, zobacz [Rozpoczynanie pracy z Magazynem obiektów blob Azure](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> Obiekty BLOB zaszyfrowane za pomocą szyfrowania po stronie klienta przechowują metadane związane z szyfrowaniem przechowywane hello obiektu blob. Jest absolutnie krytyczne, czy każdy mechanizm kopiowania zapewnił, który hello metadane obiektu blob, a szczególnie hello metadane związane z szyfrowaniem, są zachowywane. W przypadku kopiowania obiektów blob hello bez takich metadanych, hello zawartości obiektu blob nie można pobrać ponownie. Aby uzyskać więcej informacji na temat metadanych związanych z szyfrowaniem, zobacz [Azure Storage Client-Side Encryption](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Szyfrowanie po stronie klienta usługi Azure Storage).
 
## <a name="faq"></a>Często zadawane pytania

1. **Czy istniejące konta magazynu są nadal dostępne?**
   
    Tak, istniejące konta magazynu są nadal dostępne, a ich ceny i funkcje nie zostały zmienione.  Nie masz hello toochoose możliwości warstwy magazynowania, a nie mają możliwości warstw w przyszłości hello.

2. **Kiedy i dlaczego należy rozpocząć używanie kont usługi Blob Storage?**
   
    Konta magazynu obiektów blob są przeznaczone do przechowywania obiektów blob i zezwolić nam toointroduce nowe funkcje skoncentrowane obiektu blob. Idąc dalej, konta magazynu obiektów Blob to zalecany sposób przechowywania obiektów blob, ponieważ przyszłe możliwości, takie jak magazyn hierarchiczny i Obsługa poziomów hello zostaną wprowadzone na podstawie tego typu konta. Warto jednak się tooyou Jeśli chcesz toomigrate, w zależności od wymagań biznesowych.

3. **Czy przekonwertować moje istniejące konto magazynu tooa konta magazynu obiektów Blob?**
   
    Nie. Konto usługi Blob Storage to inny typ konta magazynu i należy utworzyć je na nowo, a następnie przeprowadzić migrację danych w sposób opisany powyżej.

4. **Czy mogę przechowywać obiekty w obu warstwach magazynowania w hello tego samego konta?**
   
    Witaj *"Warstwy dostępu"* atrybut wskazuje wartość hello hello warstwy magazynowania na poziomie konta i dotyczy tooall obiekty na tym koncie. Jednak hello blob warstw (wersja zapoznawcza) funkcję na poziomie umożliwi możesz tooset hello warstwy dostępu na określonych obiektów blob i spowoduje to zmianę ustawienia warstwy dostępu hello hello konta. 

5. **Czy można zmienić warstwy magazynowania hello o moim koncie magazynu obiektów Blob?**
   
    Tak. Można zmienić warstwy magazynowania hello ustawienie hello *"Warstwy dostępu"* atrybutu na powitania konta magazynu. Zmiana warstwy magazynowania hello stosuje tooall obiekty przechowywane w hello konta. Zmiana warstwy magazynu hello gorących toocool nie naliczenia żadnych opłat, gdy zmiana z toohot chłodnych pociągnąć za sobą koszt GB do odczytywania wszystkich danych hello hello konta.

6. **Jak często można zmienić warstwy magazynu hello moim koncie magazynu obiektów Blob?**
   
    Gdy firma Microsoft nie Wymuszaj ograniczenia częstotliwość można zmienić warstwy magazynowania hello, należy pamiętać, że zmiana warstwy magazynu hello z chłodnych toohot można naliczenie znaczących opłat. Zmiana warstwy magazynu hello często nie jest zalecane.

7. **Czy hello BLOB w warstwie magazynu chłodnego hello zachowywać się inaczej niż hello jedynek w hello warstwy magazynu gorącego?**
   
    Obiekty BLOB w warstwie magazynu gorącego hello mają hello takie samo opóźnienie jak obiekty BLOB na kontach magazynu ogólnego przeznaczenia. Obiekty BLOB w warstwie magazynu chłodnego hello mają podobne opóźnienie (w milisekundach) jak obiekty BLOB na kontach magazynu ogólnego przeznaczenia.
   
    Obiekty BLOB w warstwie magazynu chłodnego hello mają nieco niższy poziom dostępności usług (SLA) niż obiekty BLOB hello przechowywane w hello warstwy magazynu gorącego. Aby uzyskać więcej szczegółów, zobacz [Magazyn — umowa SLA](https://azure.microsoft.com/support/legal/sla/storage).

8. **Czy mogę przechowywać stronicowe obiekty i dyski maszyny wirtualnej na kontach usługi Blob Storage?**
   
    Konta Magazynu obiektów blob obsługują tylko blokowe obiekty blob i uzupełnialne obiekty blob — stronicowe obiekty blob nie są obsługiwane. Dyski maszyny wirtualnej Azure bazują na stronicowych obiektów blob i w związku z tym kont magazynu obiektów Blob nie może być używane toostore dysków maszyny wirtualnej. Jednak jest możliwe toostore kopie zapasowe hello dysków maszyny wirtualnej jako blokowych obiektów blob na koncie magazynu obiektów Blob.

9. **Należy toochange Moje istniejących kont magazynu obiektów Blob toouse aplikacji?**
   
    Konta Magazynu obiektów blob są w pełni spójne pod względem interfejsu API z kontami magazynu ogólnego przeznaczenia dla blokowych obiektów blob i uzupełnialnych obiektów blob. Tak długo, jak aplikacja jest używanie blokowych obiektów blob lub uzupełnialnych obiektów blob i używasz wersji 2014-02-14 hello hello [interfejsu API REST usług Storage](https://msdn.microsoft.com/library/azure/dd894041.aspx) lub większą aplikacje powinny działać. Jeśli używasz starszej wersji protokołu hello, a następnie zaktualizuj nowej wersji hello toouse aplikacji tak toowork bezproblemowo z oboma typami kont magazynu. Ogólnie rzecz biorąc zawsze zalecamy używanie hello najnowszej wersji niezależnie od tego, jaki typ konta magazynu należy użyć.

10. **Czy w środowisku użytkownika zostaną wprowadzone zmiany?**
    
    Konta magazynu obiektów blob są bardzo podobne kont magazynu ogólnego przeznaczenia tooa do przechowywania blokowych i uzupełnialnych obiektów blob i obsługują wszystkie najważniejsze funkcje hello magazynu Azure, w tym wysoka trwałość i dostępność, skalowalność, wydajność i zabezpieczeń. Inne niż hello funkcje i ograniczenia dotyczące określonych tooBlob kont magazynu i jego warstw magazynowania, które zostały wywołane powyżej wszystko else pozostaje hello takie same.

## <a name="next-steps"></a>Następne kroki

### <a name="evaluate-blob-storage-accounts"></a>Ocena konta Magazynu obiektów blob

[Sprawdzanie dostępności kont usługi Blob Storage według regionu](https://azure.microsoft.com/regions/#services)

[Ocena użycia bieżących kont magazynu przez włączenie metryk usługi Azure Storage](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Sprawdzanie cen usługi Blob Storage według regionu](https://azure.microsoft.com/pricing/details/storage/)

[Sprawdzanie ceny transferu danych](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Rozpoczynanie korzystania z kont Magazynu obiektów blob

[Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md)

[Przenoszenie tooand danych z usługi Azure Storage](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Przeglądaj i eksploruj konta magazynu](http://storageexplorer.com/)