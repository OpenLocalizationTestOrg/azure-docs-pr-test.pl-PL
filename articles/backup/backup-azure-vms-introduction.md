---
title: aaaPlanning infrastruktury kopii zapasowych maszyn wirtualnych na platformie Azure | Dokumentacja firmy Microsoft
description: "Ważne uwagi dotyczące planowania tooback zapasowych maszyn wirtualnych na platformie Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Wykonaj kopię zapasową maszyn wirtualnych, kopii zapasowych maszyn wirtualnych"
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Planowanie infrastruktury kopii zapasowych maszyny wirtualnej na platformie Azure
Ten artykuł zawiera wydajności i zasobów sugestie toohelp zaplanować infrastrukturę kopii zapasowej maszyny Wirtualnej. Definiuje również kluczowych aspektów usługi Kopia zapasowa hello; te aspekty może mieć decydujące znaczenie dla określenia architektury, planowanie pojemności i planowania. Jeśli znasz [przygotować środowisko](backup-azure-vms-prepare.md), planowania jest hello następnego kroku, przed rozpoczęciem [tooback zapasowych maszyn wirtualnych](backup-azure-vms.md). Aby uzyskać więcej informacji o maszynach wirtualnych platformy Azure, zobacz hello [dokumentacji maszyn wirtualnych](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>Jak Azure wykonywanie kopii zapasowych maszyn wirtualnych?
Gdy hello usługi Kopia zapasowa Azure inicjuje zadania tworzenia kopii zapasowej w czasie hello zaplanowane, wyzwala hello zapasowy numer wewnętrzny tootake migawki punktu w czasie. Witaj usługi Kopia zapasowa Azure korzysta hello _VMSnapshot_ rozszerzenia w systemie Windows i hello _VMSnapshotLinux_ rozszerzenia w systemie Linux. Podczas tworzenia kopii zapasowej maszyny Wirtualnej pierwszej hello zainstalowano rozszerzenia Hello. rozszerzenie hello tooinstall, musi być uruchomiona hello maszyny Wirtualnej. Jeśli hello maszyna wirtualna nie jest uruchomiona, hello usługi Kopia zapasowa tworzy migawkę hello bazowy magazynu (ponieważ nie zapisy aplikacji występuje podczas powitalne zatrzymaniu maszyny Wirtualnej).

Podczas wykonywania migawki maszyn wirtualnych systemu Windows, usługi Kopia zapasowa hello koordynuje z tooget usługi kopiowania woluminów w tle (VSS) hello spójne migawek dysków maszyny wirtualnej hello. Jeśli tworzysz kopię zapasową maszyn wirtualnych systemu Linux, można napisać własne niestandardowe skrypty tooensure spójności podczas wykonywania migawki maszyny Wirtualnej. Szczegółowe informacje na temat wywoływania tych skryptów znajdują się w dalszej części tego artykułu.

Witaj usługi Kopia zapasowa Azure wykonuje migawkę hello, hello danych po toohello przekazanych magazynu. wydajność toomaximize hello usługa identyfikuje i transferuje tylko hello bloki danych, które uległy zmianie od czasu poprzedniej kopii zapasowej hello.

![Architektura kopii zapasowych maszyny wirtualnej platformy Azure](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Po ukończeniu transferu danych hello hello migawka zostanie usunięta i utworzenia punktu odzyskiwania.

> [!NOTE]
> 1. Podczas procesu tworzenia kopii zapasowej hello kopia zapasowa Azure nie zawiera maszyny wirtualnej toohello dysku tymczasowego hello. Aby uzyskać więcej informacji, zobacz hello blog na [magazyn tymczasowy](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Ponieważ kopia zapasowa Azure przyjmuje migawki poziom miejsca do magazynowania i operacje transferu migawki toovault, nie należy zmieniać klucze konta magazynu hello zakończenie hello zadanie tworzenia kopii zapasowej.
> 3. Dla maszyn wirtualnych w warstwie premium skopiowane hello migawki toostorage konta. Jest to toomake się upewnić, że usługa Kopia zapasowa Azure pobiera wystarczające IOPS transferowania danych toovault. To dodatkowe kopię magazynu jest pobierana zgodnie z harmonogramem hello przydzielony rozmiar maszyny Wirtualnej. 
>

### <a name="data-consistency"></a>Spójność danych
Tworzenie kopii zapasowej i przywracanie krytyczne dane biznesowe jest skomplikowany hello fakt, że krytyczne dane biznesowe musi kopii zapasowej podczas aplikacji hello, które wywołują powitalne danych są uruchomione. tooaddress, kopia zapasowa Azure obsługuje spójnych z aplikacją kopii zapasowych dla systemu Windows i maszyn wirtualnych systemu Linux
#### <a name="windows-vm"></a>Maszyna wirtualna z systemem Windows
Kopia zapasowa Azure przejmuje VSS pełnych kopii zapasowych maszyn wirtualnych systemu Windows (Dowiedz się więcej o [pełna kopia zapasowa VSS](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). tooenable VSS skopiowanie kopii zapasowych, powitania po zestawie toobe potrzeb klucza rejestru na powitania maszyny Wirtualnej.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Maszyny wirtualne z systemem Linux
Kopia zapasowa Azure zapewnia platformę skryptów. tooensure spójności aplikacji, podczas tworzenia kopii zapasowej maszyn wirtualnych systemu Linux, Utwórz niestandardowe skrypty przed i po skrypty, które kontroli przepływu pracy tworzenia kopii zapasowej hello i środowiska. Kopia zapasowa Azure wywołuje skrypt wstępne hello przed wykonaniem migawki maszyny Wirtualnej hello i wywołuje skrypt po powitania po zakończeniu zadania migawki maszyny Wirtualnej hello. Aby uzyskać więcej informacji, zobacz [aplikacji spójne wirtualna kopii zapasowych przy użyciu skryptów przed i po skrypt](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> Kopia zapasowa Azure wywołuje tylko hello zapisywane klienta przed i po skryptów. Jeśli hello skryptów przed i po skryptów zostanie wykonane pomyślnie, kopia zapasowa Azure oznacza punkt odzyskiwania hello jako aplikacji spójne. Jednak powitania klienta jest odpowiedzialny hello spójności aplikacji, korzystając z niestandardowych skryptów.
>


W następującej tabeli opisano typy hello warunków spójności i hello wystąpić w podczas tworzenia kopii zapasowej maszyny Wirtualnej platformy Azure i przywrócić procedur.

| Spójność | Na podstawie usługi VSS | Objaśnienie i szczegóły |
| --- | --- | --- |
| Spójność aplikacji |Tak dla systemu Windows|Spójność aplikacji jest idealne dla obciążeń, zapewnia, że:<ol><li> Witaj wirtualna *rozruch*. <li>Brak *nie uszkodzenie*. <li>Brak *bez utraty danych*.<li> dane Hello są aplikacji toohello spójne, która używa danych hello poprzez włączenie aplikacji hello w czasie hello kopii zapasowej — za pomocą usługi VSS lub poprzedzającego utworzenie kopii zapasowej lub używanego po skryptu.</ol> <li>*Maszyny wirtualne systemu Windows*-obciążeń najbardziej firmy Microsoft ma składniki zapisywania usługi VSS, które wykonują akcje specyficznego dla obciążenia powiązanych toodata spójności. Na przykład Microsoft SQL Server ma składnik zapisywania usługi VSS, które powodują, czy plik dziennika transakcji hello zapisy toohello i hello bazy danych są wykonywane prawidłowo. Kopii zapasowych maszyny Wirtualnej systemu Windows Azure, toocreate punktów odzyskiwania zapewniających spójność aplikacji hello zapasowy numer wewnętrzny należy wywołać przepływu pracy usługi VSS hello i on zostać ukończona przed wykonaniem migawki maszyny Wirtualnej hello. Witaj maszyny Wirtualnej Azure migawki toobe dokładne składniki zapisywania usługi VSS hello wszystkich aplikacji w maszynie Wirtualnej platformy Azure należy wykonać również. (Dowiedz się hello [podstawy VSS](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) i Poznaj głębokość szczegóły hello [jej działania](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Maszyny wirtualne systemu Linux*— klienci mogą wykonywać [spójności aplikacji niestandardowych skryptów przed i po skryptu tooensure](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Spójności systemu plików |Tak — w przypadku komputerów z systemem Windows |Istnieją dwa scenariusze, w którym hello punkt odzyskiwania może być *systemu plików spójne*:<ul><li>Tworzenie kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure, bez wstępnie przygotowany-script/po-script lub jeśli wstępnie przygotowany-script/po-script nie powiodło się. <li>Błąd VSS podczas tworzenia kopii zapasowej dla maszyn wirtualnych systemu Windows na platformie Azure.</li></ul> W obu przypadkach hello najlepsze, którą można wykonać jest tooensure który: <ol><li> Witaj wirtualna *rozruch*. <li>Brak *nie uszkodzenie*.<li>Brak *bez utraty danych*.</ol> Aplikacje muszą mechanizm tooimplement własnych "konfigurowania" hello przywrócić danych. |
| Spójność awarii |Nie |Ta sytuacja jest równoważne tooa maszyny wirtualnej występuje "awarii" (za pośrednictwem zmiennego lub stałego reset). Spójność awarii zwykle odbywa się podczas zamykania hello Azure maszyny wirtualnej w czasie hello kopii zapasowej. Punkt odzyskiwania spójna w razie awarii zapewnia żadnych gwarancji wokół hello spójności danych hello na nośniku magazynowania hello — albo z punktu widzenia hello hello systemu operacyjnego lub aplikacji hello. Tylko dane hello, która już istnieje na dysku hello w czasie hello kopii zapasowej zostaną zebrane i kopii zapasowej. <br/> <br/> Gdy są zazwyczaj żadnych gwarancji, hello uruchomieniem systemu operacyjnego, a następnie sprawdzając dysku procedury, takich jak narzędzia chkdsk, toofix błędy uszkodzenia. Wszystkie dane w pamięci lub zapisy, które nie zostały przeniesione toohello dysku zostaną utracone. aplikacji Hello zazwyczaj wynika z mechanizm weryfikacji w przypadku wycofywania danych wymaga toobe gotowe. <br><br>Na przykład jeśli dziennik transakcji hello ma wpisów, które nie są dostępne w bazie danych hello, następnie hello oprogramowanie bazy danych nie wycofanie dopóki dane hello są spójne. W przypadku danych zostanie rozmieszczona na wielu dyskach wirtualnych (takich jak woluminy łączone), punkt odzyskiwania spójna w razie awarii zapewnia żadnych gwarancji pod kątem poprawności hello hello danych. |

## <a name="performance-and-resource-utilization"></a>Wydajności i użycia zasobów
Podobnie jak oprogramowanie kopii zapasowej jest wdrożony lokalnymi należy zaplanować pojemności i wykorzystania zasobów potrzeby podczas tworzenia kopii zapasowych maszyn wirtualnych na platformie Azure. Witaj [magazyn Azure ogranicza](../azure-subscription-service-limits.md#storage-limits) zdefiniuj wpływ obciążeń toorunning toostructure wirtualna wdrożeń tooget maksymalną wydajność co najmniej.

Należy zwrócić uwagę toohello, który ogranicza następujące usługi Azure Storage, podczas planowania wydajności tworzenia kopii zapasowych:

* Maksymalna liczba wyjście na konto magazynu
* Całkowita liczba żądań stawka za transakcje konta magazynu

### <a name="storage-account-limits"></a>Limity konta magazynu
Dane kopii zapasowej skopiowane z konta magazynu, dodaje toohello operacje wejścia/wyjścia na sekundę (IOPS) i transfer danych wychodzących (lub przepływności) metryki hello konta magazynu. At hello sam maszyny czasu, wirtualne zużywają również IOPS i przepustowość. Celem Hello jest tooensure kopii zapasowej i ruch maszyny wirtualnej nie może przekraczać swoje limity konta magazynu.

### <a name="number-of-disks"></a>Liczba dysków
proces tworzenia kopii zapasowej Hello możliwie jak najszybciej próbuje toocomplete zadania tworzenia kopii zapasowej. W ten sposób zużywa można dowolną liczbą zasobów. Jednak wszystkie operacje We/Wy są ograniczone przez hello *przepływność docelowy dla pojedynczego obiektu Blob*, która ma ograniczenie 60 MB na sekundę. Szybko, proces tworzenia kopii zapasowej hello próbuje — w toomaximize próba tooback hello wirtualna dysków zapasowych *równolegle*. Jeśli maszyna wirtualna ma cztery dyski, usługa hello podejmuje próby tooback się wszystkie cztery dyski równolegle. Witaj **liczba dysków** tworzona kopia zapasowa, jest hello najważniejszym czynnikiem umożliwiającym określenie ruch kopii zapasowej konta magazynu.

### <a name="backup-schedule"></a>Harmonogram tworzenia kopii zapasowych
Dodatkowy czynnik, który ma wpływ na wydajność jest hello **harmonogram tworzenia kopii zapasowych**. Jeśli możesz skonfigurować zasady hello, wszystkie maszyny wirtualne kopie zapasowe są tworzone na powitania sam czas zaplanowano zakleszczenie ruchu. proces tworzenia kopii zapasowej Hello prób tooback się wszystkie dyski równolegle. tooreduce hello kopii zapasowej ruchu z konta magazynu, wykonywanie kopii zapasowych różnych maszyn wirtualnych różnych porze dnia hello, bez nakładania się.

## <a name="capacity-planning"></a>Planowanie pojemności
Zestawienie hello poprzedniej czynników, należy tooplan na potrzeby użycia konta magazynu hello. Pobierz hello [pojemności kopii zapasowej maszyny Wirtualnej, arkusz kalkulacyjny programu Excel planowania](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) toosee hello wpływ dysku i harmonogram tworzenia kopii zapasowych wyborów.

### <a name="backup-throughput"></a>Przepustowość kopii zapasowej
Dla każdego dysku tworzona kopia zapasowa Azure Backup odczytuje hello bloków na dysku hello i magazyny hello tylko zmienione dane (przyrostowej kopii zapasowej). Hello poniższej tabeli przedstawiono wartości przepływności usługi Kopia zapasowa hello średnia. Przy użyciu hello następujące dane, można oszacować, że hello ilość czasu wymagane tooback zapasowej dysku na dany rozmiar.

| Operacja tworzenia kopii zapasowej | Najlepszym przepływności |
| --- | --- |
| Początkowa kopia zapasowa |160 MB/s |
| Przyrostowej kopii zapasowej (DR) |640 MB/s <br><br> Przepływność porzucania znacznie zmiana hello dane (wymagające toobe kopię zapasową) są rozsyłane na powitania dysku.|

## <a name="total-vm-backup-time"></a>Łączny czas tworzenia kopii zapasowej maszyny Wirtualnej
Podczas gdy większość czasu tworzenia kopii zapasowej hello jest poświęcony na odczytywanie i kopiowanie danych, innych operacji współtworzenia tooback całkowity czas potrzebny toohello zapasowej maszyny Wirtualnej:

* Czas potrzebny zbyt[Zainstaluj lub zaktualizuj zapasowy numer wewnętrzny hello](backup-azure-vms.md).
* Czas migawki jest tootrigger czas poświęcony na powitania migawki. Migawki są wyzwalane toohello Zamknij zaplanowane wykonywania kopii zapasowej.
* Czas oczekiwania w kolejce. Ponieważ usługa kopii zapasowej hello przetwarza kopii zapasowych z wielu klientów, kopiując dane kopii zapasowej z kopii zapasowej migawki toohello lub usług odzyskiwania magazynu może nie rozpocząć się natychmiast. W godzinach szczytu obciążenia oczekiwania hello można stretch się tooeight liczba godzin korzystania z powodu toohello liczbę kopii zapasowych przetwarzane. Jednak całkowity czas tworzenia kopii zapasowej hello maszyny Wirtualnej jest krótszy niż 24 godziny dla zasad tworzenia kopii zapasowych codziennie.
* Czas transferu danych, czas potrzebny do utworzenia kopii zapasowej toocompute hello przyrostowe zmiany z poprzedniej kopii zapasowej usług i przenieść magazyn toovault tych zmian.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>Dlaczego mam obserwowania longer(>12 hours) kopii zapasowej czas?
Kopia zapasowa składa się z dwóch faz: tworzenie migawek i przesyłania hello magazynu toohello migawki. optymalizuje Hello usługi Kopia zapasowa dla magazynu. Podczas przenoszenia hello migawki danych tooa magazynu, usługa hello tylko przesyła zmiany przyrostowe z hello poprzednią migawkę.  toodetermine hello przyrostowe zmiany hello usługi oblicza sumę kontrolną hello hello bloków. Zmiana bloku bloku hello jest rozpoznawany jako toobe bloku, wysyłane toohello magazynu. Następnie ćwiczenia usługi hello dalsze do każdego hello zidentyfikować bloków, wyszukiwanie tootransfer danych hello toominimize możliwości. Po przeprowadzeniu oceny wszystkie zmienione bloki, usługa hello łączy hello zmiany i wysyła je toohello magazynu. W niektórych starszych aplikacji małe, pofragmentowane zapisy nie są optymalne dla magazynu. Jeśli migawki hello zawiera wiele małych, pofragmentowane zapisy, usługa hello spędza dodatkowy czas przetwarzania danych hello napisane przez aplikacji hello. Witaj zalecane bloku zapisu aplikacji z platformy Azure, w przypadku aplikacji uruchamianych wewnątrz hello maszyny Wirtualnej, jest co najmniej 8 KB. Jeśli aplikacja korzysta z bloku mniej niż 8 KB, odbywa się wydajność tworzenia kopii zapasowej. Aby uzyskać pomoc dotyczącą dostrajania wydajności tworzenia kopii zapasowych tooimprove aplikacji, zobacz [Dostrajanie aplikacji, aby uzyskać optymalną wydajność z usługą Azure storage](../storage/common/storage-premium-storage-performance.md). Chociaż artykuł hello na wydajność tworzenia kopii zapasowej używa przykłady magazynu Premium, wskazówki hello dotyczy dyski magazynu w warstwie standardowa.

## <a name="total-restore-time"></a>Przywracanie całkowity czas
Operacja przywracania składa się z dwóch zadań main sub: kopiowanie danych z konta magazynu hello magazynu toohello wybranego klienta i tworzenie maszyny wirtualnej hello. Kopiowanie danych z magazynu hello zależy od tego, gdzie hello kopie zapasowe są wewnętrznie przechowywane na platformie Azure i przechowywania konta magazynu powitania klienta. Czas poświęcony na toocopy danych zależy od:
* Czas — oczekiwania w kolejce ponieważ hello usługa przetwarza przywrócić zadania z wielu klientów na powitania tym samym czasie, przywracanie żądania są umieszczone w kolejce.
* Czas — kopiowania danych dane są kopiowane z konta magazynu hello magazynu toohello klienta. Przywróć czas zależy od IOPS i pobiera przepływności usługi Kopia zapasowa Azure na koncie magazynu wybrane powitania klienta. tooreduce hello kopiowanie czas podczas procesu przywracania hello, wybierz konto magazynu nie został załadowany z innych aplikacji zapisami i odczytami.

## <a name="best-practices"></a>Najlepsze praktyki
Sugerujemy następujące te wskazówki podczas konfigurowania kopii zapasowych maszyn wirtualnych:

* Nie zaplanować więcej niż 10 klasycznych maszyn wirtualnych z hello takie same w chmurze usługi tooback na powitania tym samym czasie. Jeśli chcesz tooback się wiele maszyn wirtualnych z tej samej usługi w chmurze, przesunąć godziny rozpoczęcia tworzenia kopii zapasowej hello o godzinę.
* Nie należy planować więcej niż 40 tooback maszyn wirtualnych się na powitania tym samym czasie.
* Planowanie kopii zapasowych maszyn wirtualnych podczas godziny poza szczytem. Ten sposób hello usługi Kopia zapasowa używa IOPS do przesyłania danych z powitania klienta magazynu konta toohello.
* Upewnij się, że zasady są stosowane na maszynach wirtualnych umieszczonych na różnych kont magazynu. Zalecamy nie więcej niż 20 całkowita liczba dysków z konta magazynu pojedynczego chronione za pomocą hello sam harmonogram tworzenia kopii zapasowej. Jeśli masz ponad 20 dysków na koncie magazynu rozkładu tych maszyn wirtualnych między wieloma zasadami tooget hello wymagane IOPS fazie transfer hello hello procesu tworzenia kopii zapasowej.
* Nie należy przywracać maszyny Wirtualnej z systemem na koncie magazynu toosame magazynu Premium. Jeśli proces operacji przywracania hello pokrywa się z operacją tworzenia kopii zapasowej hello, zmniejsza hello dostępne IOPS dla kopii zapasowej.
* Dla kopii zapasowej maszyny Wirtualnej — wersja Premium upewnij się, że dysków premium hostów ma co najmniej 50% wolnego miejsca do przemieszczania migawki do pomyślnego utworzenia kopii zapasowej konto magazynu. 
* Upewnij się, że ta wersja języka python na maszynach wirtualnych systemu Linux włączone dla kopii zapasowej jest 2.7

## <a name="data-encryption"></a>Szyfrowanie danych
Kopia zapasowa Azure nie szyfruje danych jako część procesu tworzenia kopii zapasowej hello. Jednak można zaszyfrować dane w ramach hello maszyny Wirtualnej i Utwórz kopię zapasową hello chronione dane bezproblemowo (Dowiedz się więcej o [tworzenie kopii zapasowych danych zaszyfrowanych](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Obliczanie kosztu hello wystąpienia chronione
Maszyny wirtualne platformy Azure, których kopie zapasowe są tworzone za pomocą usługi Kopia zapasowa Azure podlegają zbyt[cennikiem usługi Kopia zapasowa Azure](https://azure.microsoft.com/pricing/details/backup/). Hello obliczania chronione wystąpienia jest oparta na powitania *rzeczywiste* rozmiarze hello maszynę wirtualną, która jest równa sumie hello wszystkie dane hello w maszynie wirtualnej hello — z wyjątkiem hello "zasobu dysku".

Cennik wykonywanie kopii zapasowych maszyn wirtualnych jest *nie* hello maksymalny obsługiwany rozmiar maszyn wirtualnych toohello dołączone dysku danych. Cennik jest oparta na hello rzeczywiste dane przechowywane w hello dysku danych. Podobnie rachunku magazynu kopii zapasowych hello jest oparta na powitania ilość danych przechowywanych w kopia zapasowa Azure, czyli hello sumę hello rzeczywiste dane w każdym punkcie odzyskiwania.

Na przykład zająć A2 standardowy rozmiar maszyny wirtualnej, która ma dwa dyski dodatkowe dane o maksymalnym rozmiarze 1 TB. Witaj poniższej tabeli przedstawiono hello rzeczywiste dane przechowywane na każdym z tych dysków:

| Typ dysku | Maksymalny rozmiar | Rzeczywiste dane. |
| --- | --- | --- |
| Dysk systemu operacyjnego |1023 GB |17 GB |
| Dysk lokalny / zasobu dysku |135 GB |5 GB (nie uwzględniony w kopii zapasowej) |
| Dysk danych 1 |1023 GB |30 GB |
| Dysk z danymi 2 |1023 GB |0 GB |

Witaj *rzeczywiste* rozmiar maszyny wirtualnej hello jest w tym przypadku 17 GB + 30 GB + 0 GB = 47 GB. Ten rozmiar chronione wystąpienia (47 GB) staje się hello podstawę rachunek miesięczny hello. Jako hello ilości danych na maszynie wirtualnej hello rozwojem rozmiar chronione wystąpienia hello używane przy zmianach rozliczeń odpowiednio.

Nie można uruchomić rozliczeń, aż do zakończenia hello pierwszym pomyślnym utworzeniu kopii. W tym momencie rozpoczyna się hello rozliczeń dla magazynu i chronione wystąpienia. Karta będzie kontynuowane tak długo, jak istnieje *dowolnej kopii zapasowej danych przechowywanych w magazynie* hello maszyny wirtualnej. Jeśli użytkownik zaprzestanie ochrony na maszynie wirtualnej hello, ale dane kopii zapasowej maszyny wirtualnej istnieje w magazynie, nadal rozliczeń.

Rozliczeń dla określonej maszyny wirtualnej zatrzymuje tylko wtedy, gdy ochrona powitalnych jest zatrzymana *i* wszystkie dane kopii zapasowej zostaną usunięte. Po zatrzymaniu ochrony i nie istnieją aktywne zadania tworzenia kopii zapasowej, rozmiar chronione wystąpienia hello używany dla rachunek miesięczny hello staje się rozmiar hello hello ostatniego pomyślnego kopii zapasowej maszyny Wirtualnej.

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Następne kroki
* [Tworzenie kopii zapasowych maszyn wirtualnych](backup-azure-vms.md)
* [Zarządzanie kopiami zapasowymi maszyny wirtualnej](backup-azure-manage-vms.md)
* [Przywracanie maszyn wirtualnych](backup-azure-restore-vms.md)
* [Rozwiązywanie problemów kopii zapasowej maszyny Wirtualnej](backup-azure-vms-troubleshoot.md)
