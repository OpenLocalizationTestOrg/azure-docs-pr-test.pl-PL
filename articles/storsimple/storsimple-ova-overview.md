---
title: "Omówienie tablicy wirtualnych Azure StorSimple aaaMicrosoft | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello tablicy wirtualnego StorSimple, zintegrowane pamięci masowej zarządzanego zadań magazynu między lokalnymi tablicy wirtualnych i magazynu w chmurze Microsoft Azure."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Wprowadzenie toohello tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie
Hello tablicy wirtualne Microsoft Azure StorSimple to rozwiązanie zintegrowanego magazynu zarządzanego zadań magazynu między lokalnymi tablicy wirtualny działający w funkcji hypervisor i magazynu w chmurze Microsoft Azure. Tablica wirtualnego Hello jest serwer plików wydajne, ekonomiczne i łatwe do zarządzania lub rozwiązania z serwerem iSCSI, która eliminuje wiele problemów hello i koszty związane z ochroną magazyn i dane przedsiębiorstwa. Tablica wirtualnego Hello jest szczególnie nadają się do scenariuszach dotyczących biura zdalnego/oddział.

Ten temat zawiera omówienie wirtualnych tablicy hello — poniżej przedstawiono niektóre inne zasoby:

* Aby uzyskać najlepsze rozwiązania, zobacz [najlepsze rozwiązania w zakresie tablicy wirtualnego StorSimple](storsimple-ova-best-practices.md).
* Omówienie urządzeń z serii StorSimple 8000 hello Przejdź zbyt[z serii StorSimple 8000: rozwiązanie chmury hybrydowej](storsimple-overview.md). 
* Aby uzyskać informacje dotyczące urządzeń z serii StorSimple 5000/7000 hello, przejdź zbyt[pomocy Online StorSimple](http://onlinehelp.storsimple.com/).

Tablica wirtualnego Hello obsługuje hello iSCSI lub protokołu bloku komunikatów serwera (SMB). Go działa w istniejącej infrastrukturze funkcji hypervisor i udostępnia warstw chmury toohello, kopia zapasowa w chmurze szybkiego przywracania, odzyskiwania na poziomie elementu i funkcje odzyskiwania po awarii.

Witaj Poniższa tabela zawiera podsumowanie hello ważne funkcje hello tablicy wirtualne StorSimple.

| Funkcja | Macierz wirtualna usługi StorSimple |
| --- | --- |
| Wymagania dotyczące instalacji |Używa infrastruktury wirtualizacji (funkcja Hyper-V lub programu VMware) |
| Dostępność |Jeden węzeł |
| Łączna pojemność (w tym chmury) |Zdolności too64 TB można używać na tablicę wirtualnego |
| Wydajność lokalnej |390 GB too6.4 TB pojemności można używać na tablicę wirtualnych (potrzeby tooprovision 500 GB too8 TB miejsca na dysku) |
| Protokoły natywnego |SMB lub iSCSI |
| Cel czasu odzyskiwania (recovery time objective, RTO) |iSCSI: mniej niż 2 minuty, niezależnie od rozmiaru |
| Cel punktu odzyskiwania (recovery point objective, RPO) |Codzienne wykonywanie kopii zapasowych i kopii zapasowych na żądanie |
| Warstwy magazynowania |Używa ogrzewać toodetermine mapowania, jakie dane powinna należeć do warstwy przychodzący lub wychodzący |
| Pomoc techniczna |Obsługiwane przez dostawcę hello infrastruktury wirtualizacji |
| Wydajność |Może być różna w zależności od podstawowej infrastruktury |
| Przenoszenia danych |Można przywrócić toohello tego samego urządzenia lub na poziomie elementu recovery (serwer plików) |
| Warstwy magazynowania |Magazyn lokalnych i w chmurze |
| Rozmiar udziału |Warstwowe: zapasowej too20 TB; przypięty lokalnie: Konfigurowanie too2 TB |
| Rozmiar woluminu |Warstwowe: TB too5 500 GB; przypięty lokalnie: 50 GB too500 GB |
| Rozmiar woluminu |Warstwowe: zapasowej too5 TB; przypięty lokalnie: Konfigurowanie too500 GB |
| Migawki |Awarii |
| Odzyskiwanie na poziomie elementu |Tak; Użytkownicy mogą przywracać z udziałów |

## <a name="why-use-storsimple"></a>Dlaczego warto używać StorSimple?
StorSimple łączy użytkowników i serwerów tooAzure magazynu (w minutach) bez żadnych modyfikacji aplikacji.

Hello poniższej tabeli opisano niektóre najważniejsze zalety hello tego hello StorSimple tablicy wirtualnych zapewnia rozwiązanie.

| Funkcja | Korzyść |
| --- | --- |
| Integracja przezroczyste |Tablica wirtualnego Hello obsługuje hello protokołu SMB lub hello iSCSI. Hello przenoszenia danych między warstwą lokalne powitania i warstwy chmury hello jest użytkownikiem toohello łatwego i przezroczysty. |
| Magazyn zmniejszenie kosztów |StorSimple należy zapewnić obsługę administracyjną wystarczający Magazyn lokalny toomeet bieżącego zapotrzebowanie na powitania najczęściej używane gorących danych. Potrzeb magazynu powiększania, StorSimple warstw zimnych danych do ekonomicznego chmury magazynu. Witaj danych jest deduplikowany i skompresowane przed wysłaniem chmury toohello toofurther zmniejszyć wymagania dotyczące magazynu i kosztów. |
| Uproszczone zarządzanie magazynem |StorSimple umożliwia scentralizowane zarządzanie w chmurze hello przy użyciu Menedżera urządzeń StorSimple toomanage wielu urządzeń. |
| Ulepszonych funkcji odzyskiwania i zgodność |StorSimple umożliwia szybsze odzyskiwanie po awarii przez Przywracanie metadanych hello natychmiast i przywracanie danych hello, zgodnie z potrzebami. Oznacza to, że minimalnego przerw w działaniu można kontynuować wykonywania normalnych operacji. |
| Przenoszenia danych |Dane, które toohello warstwowych chmury można uzyskać z innych witryn do celów odzyskiwania i migracji. Należy pamiętać, można przywrócić tylko toohello oryginalny wirtualny tablica danych. Jednak użyć awaryjnego odzyskiwania funkcji toorestore hello cały wirtualny tablicy tooanother wirtualnego tablicy. |

## <a name="storsimple-workload-summary"></a>Podsumowanie obciążenia StorSimple

Podsumowanie obsługiwanych obciążeniach StorSimple jest przedstawione w poniższej tabeli.

|Scenariusz     |Obciążenie     |Obsługiwane      |Ograniczenia               |
|-------------|-------------|---------------|---------------------------|
|Współpraca ROBO |Udostępnianie plików     |Tak      |Zobacz [maksymalnych dla serwera plików](storsimple-ova-limits.md).<br></br>Zobacz [wymagania systemowe dotyczące obsługiwanych wersji protokołu SMB](storsimple-ova-system-requirements.md).| Wszystkie wersje     |

## <a name="workflows"></a>Przepływy
Witaj tablicy wirtualnego StorSimple szczególnie nadaje się do powitania po przepływy pracy:

* [Zarządzanie magazynami oparte na chmurze](#cloud-based-storage-management)
* [Niezależnym od lokalizacji kopii zapasowej](#location-independent-backup)
* [Dane ochrony i odzyskiwania po awarii](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>Zarządzanie magazynami oparte na chmurze
Można użyć hello Menedżera urządzeń StorSimple usługa jest uruchomiona w hello Azure portalu toomanage danych przechowywanych na wielu urządzeniach i w wielu lokalizacjach. Jest to szczególnie przydatne w scenariuszach oddziału rozproszonych. Należy pamiętać, że należy utworzyć oddzielne wystąpienia tablice wirtualnego usługi toomanage hello Menedżera urządzeń StorSimple i fizyczne urządzenia StorSimple. Należy również zauważyć hello tablicy wirtualnych używa teraz hello nowego portalu Azure zamiast hello klasycznego portalu Azure.

![Zarządzanie magazynami oparte na chmurze](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Niezależnym od lokalizacji kopii zapasowej
Z tablicą wirtualnego hello migawki w chmurze dostarcza niezależnym od lokalizacji, w momencie kopię woluminu lub udziału. Migawki w chmurze są domyślnie włączone i nie można wyłączyć. Wszystkie woluminy i udziały są kopii zapasowej w górę na powitania sam czas za pośrednictwem jednej zasady tworzenia kopii zapasowej codziennie, i należy wykonać dodatkowe ad hoc kopii zapasowych, gdy jest to niezbędne.

### <a name="data-protection-and-disaster-recovery"></a>Dane ochrony i odzyskiwania po awarii
Tablica wirtualnego Hello obsługuje hello następujące scenariusze odzyskiwania danych ochrony i odzyskiwaniem po awarii:

* **Przywracanie woluminu lub udziału** — użyj polecenia hello restore jako nowego przepływu pracy toorecover woluminu lub udziału. Użyj tego podejścia toorecover hello całego woluminu lub udziału.
* **Element poziomu odzyskiwania** — udziałów zezwolić na dostęp uproszczony toorecent kopii zapasowych. Można łatwo odzyskać pojedynczy plik z specjalnego *.backup* folderów, które są dostępne w chmurze hello. Ta funkcja przywracania jest oparte na użytkownika i administracyjne interwencja nie jest wymagane.
* **Odzyskiwanie po awarii** — Użyj hello toorecover możliwości trybu failover, wszystkie woluminy lub udziały tooa nowy wirtualny tablicy. Można utworzyć nowej tablicy wirtualnego hello zarejestrowanie go za pomocą hello usługi Menedżer StorSimple urządzenia, a następnie w tryb failover hello oryginalny wirtualny tablicy. nowy wirtualny tablicy Hello następnie przyjmie założenie hello udostępnione zasoby. 

## <a name="storsimple-virtual-array-components"></a>Składniki tablicy wirtualnego StorSimple
Tablica wirtualnego Hello obejmuje hello następujące składniki:

* [Tablica wirtualnego](#virtual-array) — urządzenie magazynujące hybrydowe chmury oparte na maszynie wirtualnej, udostępnione w środowisku zwirtualizowanym lub funkcji hypervisor.  
* [Usługa Menedżera urządzeń StorSimple](#storsimple-device-manager-service) — jako rozszerzenie hello portalu Azure, która umożliwia zarządzanie co najmniej jedno urządzenie StorSimple z interfejsu jednej sieci web, którego można korzystać z położeniem geograficznym. Można użyć toocreate usługi Menedżer StorSimple urządzenia hello i zarządzania usługami, wyświetlić i zarządzanie urządzeniami i alertami i zarządzanie woluminów, udziałów i migawek istniejącej.
* [Interfejs użytkownika sieci web lokalnego](#local-web-user-interface) — oparte na sieci web interfejsu użytkownika, który jest używany tooconfigure hello urządzenia, dzięki czemu można połączyć sieć lokalną toohello i zarejestruj urządzenie hello usługi Menedżer StorSimple urządzenia hello. 
* [Interfejs wiersza polecenia](#command-line-interface) — interfejsu programu Windows PowerShell, na powitania wirtualnego tablicy można toostart sesji pomocy technicznej.
  Witaj poniższych sekcjach opisano każdy z tych składników bardziej szczegółowo i wyjaśniono sposób rozwiązania hello rozmieszcza danych przydziela magazynu i ułatwia zarządzanie magazynami i ochrony danych.

### <a name="virtual-array"></a>Macierz wirtualna
Tablica wirtualnego Hello jest rozwiązanie magazynu z jednym węzłem, które zapewnia magazynu głównego i zarządza komunikacją z magazynu w chmurze oraz ułatwia tooensure hello zabezpieczeń i poufności wszystkich danych przechowywanych na urządzeniu hello.

Tablica wirtualnego Hello jest dostępne w jednym modelu, który jest dostępny do pobrania. Tablica wirtualnego Hello ma maksymalną pojemność 6,4 TB na powitania urządzenia (z podstawowej wymaganie magazynu o rozmiarze 8 TB) i, w tym 64 TB magazynu w chmurze. 

Tablica wirtualnego Hello ma hello następujące funkcje:

* Jest kosztowne. Go sprawia, że wykorzystanie istniejącej infrastruktury wirtualizacji i może zostać wdrożony w sieci istniejących funkcji hypervisor Hyper-V lub VMware.
* Znajduje się w centrum danych hello, a może być skonfigurowany jako serwer iSCSI lub na serwerze plików. 
* Jest zintegrowany z chmurą hello.
* Kopie zapasowe są przechowywane w chmurze hello, która może ułatwić odzyskiwanie po awarii i uprościć odzyskiwanie na poziomie elementu (ILR). 
* Można stosować aktualizacje toohello wirtualnego tablicy, tak samo, jak spowoduje ich zastosowania tooa urządzenia fizycznego.

> [!NOTE]
> Nie można rozwijać wirtualnego tablicy. Dlatego jest ważne tooprovision odpowiedniego magazynu podczas tworzenia hello wirtualnego tablicy. 
> 
> 

### <a name="storsimple-device-manager-service"></a>Usługa menedżera urządzenia StorSimple
Microsoft Azure StorSimple udostępnia interfejs użytkownika sieci web hello usługę Menedżer urządzeń StorSimple, które umożliwia toocentrally możesz zarządzać magazynem StorSimple. Program hello Menedżera urządzeń StorSimple usługi tooperform hello następujące zadania:

* Zarządzanie wiele tablic wirtualnych StorSimple z jednej usługi. 
* Konfigurowanie i zarządzanie ustawieniami zabezpieczeń dla tablic wirtualne StorSimple. (Szyfrowanie w chmurze hello jest zależna od interfejsów API usługi Microsoft Azure).
* Konfigurowanie poświadczeń konta magazynu i właściwości.
* Konfigurowanie i zarządzanie nimi woluminy lub udziały.
* Tworzenie kopii zapasowej i przywracania danych na woluminy lub udziały.
* Monitorowanie wydajności.
* Przejrzyj ustawienia systemu i identyfikowania potencjalnych problemów.

Możesz użyć hello Menedżera urządzeń StorSimple usługi tooperform codzienne zadania administracyjne macierzy wirtualnego.

Aby uzyskać więcej informacji, przejdź zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Interfejs użytkownika sieci web lokalnego
Tablica wirtualnego Hello obejmuje opartych na sieci web interfejsu użytkownika, który jest używany do jednorazowej konfiguracji i rejestracji urządzenie hello hello usługi Menedżer StorSimple urządzenia. Można można użyć tooshut w dół i ponownego uruchomienia wirtualnych tablicy hello, uruchamiania testów diagnostycznych aktualizacji oprogramowania, Zmień hasło administratora urządzenia hello, sprawdź dzienniki systemu i skontaktuj się z Microsoft Support toofile żądania obsługi. 

Informacji o używaniu hello opartych na sieci web interfejsu użytkownika, należy przejść za[Użyj hello tooadminister interfejsu użytkownika sieci web tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Interfejs wiersza polecenia
uwzględnione Hello interfejsu programu Windows PowerShell umożliwia tooinitiate sesję pomocy technicznej z Microsoft Support, dzięki czemu mogą one pomóc rozwiązywania oraz usuwania problemów, które mogą wystąpić w sieci wirtualnej macierzy.

## <a name="storage-management-technologies"></a>Technologie magazynowania zarządzania
Ponadto toohello tablicy wirtualnych i inne składniki hello StorSimple używa rozwiązania hello następującego oprogramowania technologii tooprovide szybki dostęp tooimportant danych, zmniejszenia użycia magazynu i ochrony danych znajdujących się w sieci wirtualnej macierzy:

* [Warstwy magazynowania automatyczne](#automatic-storage-tiering) 
* [I woluminów przypiętych lokalnie udziałów](#locally-pinned-shares-and-volumes)
* [Na potrzeby deduplikacji i kompresji danych do warstwy lub kopii zapasowej toohello chmury](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Tworzenie kopii zapasowych zaplanowanych, jak i na żądanie](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Warstwy magazynowania automatyczne
Hello wirtualnego tablicy używa warstw danych toomanage przechowywane mechanizmu na powitania wirtualnego chmury tablicy i hello. Istnieją tylko dwa warstw: tablicy wirtualnego lokalne powitania i Azure magazynu w chmurze. Hello tablicy wirtualnego StorSimple automatycznie rozmieszcza warstw hello oparte na mapie interakcji śledzi bieżące dane użycia, wieku i relacje tooother danych. Dane, które są najbardziej aktywnych (najnowszych) są przechowywane lokalnie, gdy mniej aktywnych i nieaktywnych dane są automatycznie migrowane toohello chmury. (Wszystkie kopie zapasowe są przechowywane w chmurze hello). StorSimple można dostosować i Reorganizuje dane i zmień przydziałów magazynowania jako wzorców użycia. Na przykład niektóre informacje mogą stać się mniej aktywne w czasie. Ponieważ staje się stopniowo mniej aktywne, jest warstwowa limit toohello chmury. Jeśli ten sam danych stanie się ponownie aktywna, jest warstwowa toohello tablicy magazynowej.

Dane dla danego udziału warstwowych lub woluminu jest gwarantowana własną przestrzeń warstwie lokalnej. (około 10% hello całkowitej ilości miejsca zainicjowana dla tego udziału lub wolumin). Podczas zmniejsza hello dostępnego magazynu w macierzy wirtualnego hello na tym udziale lub woluminie, gwarantuje to, że obsługa poziomów dla jednego udziału lub wolumin nie wpłynie hello warstw potrzeb inne udziały lub woluminy. W związku z tym bardzo zajęty obciążenie jednego udziału lub wolumin nie może wymusić wszystkich innych chmury toohello obciążeń. 

![Warstwy magazynowania automatyczne](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> Można określić wolumin przypięty lokalnie, w takim przypadku hello danych pozostaje w macierzy wirtualnego hello i nigdy nie jest do warstwy toohello chmury. Aby uzyskać więcej informacji, przejdź zbyt[przypięty lokalnie, woluminów i udziałów](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>I woluminów przypiętych lokalnie udziałów
Możesz utworzyć odpowiednie udziały i woluminy przypięte lokalnie. Ta funkcja gwarantuje, że dane wymagane przez aplikacje krytyczne pozostaje w tablicy wirtualnego hello i nigdy nie jest do warstwy toohello chmury. Udziały przypiętych lokalnie i woluminy mają hello następujące funkcje: 

* Nie są one opóźnienia toocloud podmiotu lub problemów z łącznością.
* One nadal korzystać z StorSimple chmury kopii zapasowych i odzyskiwaniem po awarii funkcji odzyskiwania.

Można przywrócić udziału przypiętych lokalnie lub woluminie warstwowej lub warstwowych udziału lub przypięty lokalnie woluminu. 

Aby uzyskać więcej informacji na temat woluminów przypiętych lokalnie Przejdź zbyt[korzysta z woluminów toomanage usługi Menedżer StorSimple urządzenia hello](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>Na potrzeby deduplikacji i kompresji danych do warstwy lub kopii zapasowej toohello chmury
StorSimple używa deduplikacji i dane kompresji toofurther zmniejszyć wymagania dotyczące magazynu w chmurze hello. Deduplikacji zmniejsza hello ogólną ilość danych przechowywanych przez wyeliminowanie nadmiarowości w zestawie danych hello przechowywane. Informacje zmian, StorSimple ignoruje hello bez zmian danych i przechwytywania hello tylko zmiany. Ponadto StorSimple zmniejsza hello ilość przechowywanych danych identyfikowanie i usuwając zduplikowane informacje. 

> [!NOTE]
> Dane przechowywane na powitania wirtualnego tablicy nie jest deduplikowany lub skompresowany. Wszystkie deduplikacji i kompresji występuje tuż przed hello dane są przesyłane toohello chmury.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Tworzenie kopii zapasowych zaplanowanych, jak i na żądanie
Funkcje ochrony danych StorSimple umożliwiają tworzenie kopii zapasowych toocreate na żądanie. Ponadto domyślny harmonogram tworzenia kopii zapasowej zapewnia, że jest wykonywana kopia zapasowa codziennie danych. Kopie zapasowe są pobierane w postaci hello migawek przyrostowe, które są przechowywane w chmurze hello. Migawki, w których rejestrowane tylko hello zmiany od ostatniej kopii zapasowej hello, można tworzyć i szybko przywrócić. Te migawki może być bardzo ważny w scenariuszach odzyskiwania po awarii, ponieważ zastąpić systemy dodatkowej magazynu (na przykład kopii zapasowej na taśmie) i umożliwić toorestore danych tooyour centrum danych lub tooalternate witryn w razie potrzeby.

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[przygotowanie hello tablicy wirtualny portalu](storsimple-virtual-array-deploy1-portal-prep.md).

