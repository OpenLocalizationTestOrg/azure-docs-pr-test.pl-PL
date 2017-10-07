---
title: aaaWhat jest StorSimple Snapshot Manager? | Microsoft Docs
description: Opisuje hello StorSimple Snapshot Manager, jego architektury i jego funkcje.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Wprowadzenie tooStorSimple Snapshot Manager

## <a name="overview"></a>Omówienie
StorSimple Snapshot Manager jest przystawką Microsoft Management Console (MMC), która ułatwia ochronę danych i zarządzania kopiami zapasowymi w środowisku Microsoft Azure StorSimple. StorSimple Snapshot Manager można zarządzać danych Microsoft Azure StorSimple w centrum danych hello i w chmurze hello jako pojedynczy magazyn zintegrowanego rozwiązania, w związku z tym uproszczeniu procesów tworzenia kopii zapasowej i zmniejszenie kosztów.

To omówienie wprowadza hello StorSimple Snapshot Manager, opisano jego funkcji i wyjaśniono swoją rolę w Microsoft Azure StorSimple. 

Omówienie hello całego systemu Microsoft Azure StorSimple systemu, w tym urządzenia StorSimple hello, usługi Menedżer StorSimple, StorSimple Snapshot Manager i karty StorSimple dla programu SharePoint, zobacz [z serii StorSimple 8000: chmura hybrydowa rozwiązanie magazynowania](storsimple-overview.md). 

> [!NOTE]
> * Nie można użyć toomanage StorSimple Snapshot Manager Microsoft Azure StorSimple wirtualnego tablic (znanej także jako StorSimple lokalnego urządzenia wirtualnego).
> * Jeśli planujesz tooinstall StorSimple Update 2 na urządzeniu StorSimple można się toodownload hello najnowszej wersji programu StorSimple Snapshot Manager i zainstalować ją **przed zainstalowaniem StorSimple Update 2**. Witaj najnowszej wersji programu StorSimple Snapshot Manager jest zgodne z poprzednimi wersjami i działa w przypadku wszystkich wersji wydanej programu Microsoft Azure StorSimple. Jeśli używasz hello poprzedniej wersji programu StorSimple Snapshot Manager, należy tooupdate it (nie trzeba toouninstall hello poprzedniej wersji przed zainstalowaniem nowej wersji hello).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Cel StorSimple Snapshot Manager i architektura
StorSimple Snapshot Manager udostępnia centralną konsolę zarządzania użyciem toocreate spójne, kopie zapasowe w momencie lokalnych i chmurze danych. Na przykład można użyć konsoli hello:

* Konfigurowanie, tworzenie kopii zapasowej i usuwanie woluminów.
* Skonfiguruj wolumin tooensure grupy, którego kopię zapasową danych jest spójne z aplikacjami.
* Zarządzanie zasad tworzenia kopii zapasowych, dzięki czemu jest wykonywana kopia zapasowa danych na uprzednio określonym harmonogramem.
* Utwórz lokalne i migawki, które mogą być przechowywane w chmurze hello lub używanych na potrzeby odzyskiwania po awarii w chmurze.

Witaj StorSimple Snapshot Manager pobiera hello listę aplikacji, w zarejestrowany dostawca usługi VSS hello na powitania hosta. Następnie toocreate spójnych z aplikacją kopii zapasowych, sprawdza woluminy hello używany przez aplikację, a także sugeruje tooconfigure grup woluminu. StorSimple Snapshot Manager korzysta z tych woluminów grup toogenerate kopii zapasowych, które są spójne z aplikacjami. (Spójności aplikacji występuje, gdy wszystkie powiązane pliki i baz danych są zsynchronizowane i reprezentują hello rzeczywisty stan aplikacji hello w określonym punkcie w czasie.) 

Kopie zapasowe programu StorSimple Snapshot Manager zająć hello formę przyrostowe migawki, które umożliwiają przechwytywanie tylko hello zmiany od ostatniej kopii zapasowej hello. W związku z tym kopie zapasowe wymagają mniejszej ilości pamięci i można tworzyć i szybko przywrócić. StorSimple Snapshot Manager używa tooensure usługi kopii tle (VSS) systemu Windows woluminu hello aby migawki przechwytywania danych spójnych z aplikacją. (Aby uzyskać więcej informacji, przejdź toohello integracji z sekcji usługi kopiowania woluminów w tle systemu Windows). StorSimple Snapshot Manager można utworzyć harmonogramy tworzenia kopii zapasowej lub korzystać z bezpośrednim kopii zapasowych zgodnie z potrzebami. Jeśli potrzebujesz toorestore dane z kopii zapasowej, umożliwia StorSimple Snapshot Manager wybierz z katalogu lokalnego lub migawki w chmurze. Azure StorSimple przywraca tylko hello danych jest wymagany, ponieważ jest to potrzebne, która zapobiega opóźnieniom danych są dostępne podczas operacji przywracania).

![Architektura programu StorSimple Snapshot Manager](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Architektura programu StorSimple Snapshot Manager** 

## <a name="support-for-multiple-volume-types"></a>Obsługa wielu typów woluminu
Można użyć hello tooconfigure StorSimple Snapshot Manager i utworzyć kopię zapasową hello następujące typy woluminów: 

* **Woluminy podstawowe** — woluminu podstawowego jest jednej partycji na dysku podstawowym. 
* **Woluminów prostych** — prosty wolumin jest dynamiczny wolumin, który zawiera miejsca na dysku na pojedynczym dysku dynamicznego. Wolumin prosty składa się z jednego regionu na dysku lub w wielu regionach, które są połączone ze sobą na hello tego samego dysku. (Woluminy proste można tworzyć tylko na dyskach dynamicznych.) Nie są odporne na uszkodzenia.
* **Woluminy dynamiczne** — wolumin dynamiczny jest wolumin utworzony na dysku dynamicznym. Dyski dynamiczne Użyj tootrack informacje o bazie danych o woluminach, które znajdują się na dyski dynamiczne w komputerze. 
* **Woluminy dynamiczne dublowanie** — woluminy dynamiczne dublowanie są tworzone w oparciu o architekturę hello RAID 1. Z macierzy RAID 1 identyczne dane są zapisywane na dysku co najmniej dwa produkujących dublowany zestaw. Żądanie odczytu następnie są obsługiwane przez każdego dysku, który zawiera hello żądanych danych.
* **Udostępnione woluminy klastra** — z udostępnione woluminy klastra (CSV), wiele węzłów w klastrze trybu failover można jednocześnie odczytu lub zapisu toohello tego samego dysku. Tryb failover z jednym węzłem tooanother węzła może wystąpić szybko, bez konieczności zmiany własności dysku lub instalowanie, odinstalowywanie i usuwanie woluminu. 

> [!IMPORTANT]
> Nie można mieszać udostępnionych woluminów klastra i z systemem innym niż CSV w hello tego samego migawki. Mieszanie udostępnionych woluminów klastra i z systemem innym niż CSV migawki nie jest obsługiwane. 
> 
> 

Można użyć grup całego woluminu StorSimple Snapshot Manager toorestore lub sklonować poszczególnych woluminów i odzyskanie poszczególnych plików.

* [Woluminy i grup woluminu](#volumes-and-volume-groups) 
* [Typy kopii zapasowych i zasady tworzenia kopii zapasowej](#backup-types-and-backup-policies) 

Aby uzyskać więcej informacji o funkcjach programu StorSimple Snapshot Manager i toouse, zobacz temat [interfejsu użytkownika programu StorSimple Snapshot Manager](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Woluminy i grup woluminu
StorSimple Snapshot Manager tworzyć woluminy i skonfigurować je w grupach woluminu. 

StorSimple Snapshot Manager korzysta z woluminu grup toocreate kopii zapasowych, które są spójne z aplikacjami. Spójności aplikacji występuje, gdy wszystkie powiązane pliki i baz danych są zsynchronizowane i reprezentują hello rzeczywisty stan aplikacji w określonym punkcie w czasie. Wolumin grup (które są nazywane również *spójności grup*) podstawa hello tworzenia kopii zapasowej lub przywracania zadania.

Grupy woluminu nie są hello taki sam jak kontenery woluminów. Kontener woluminów zawiera jeden lub więcej woluminów, które mają konta magazynu w chmurze i inne atrybuty, takie jak szyfrowanie oraz przepustowości łącza. Kontener pojedynczy wolumin może zawierać zapasowe woluminów StorSimple too256 alokowane elastycznie. Aby uzyskać więcej informacji na temat kontenery woluminów Przejdź zbyt[Zarządzanie kontenerów woluminu](storsimple-manage-volume-containers.md). Wolumin grupy są kolekcjami elementów woluminów skonfigurowanie toofacilitate operacje tworzenia kopii zapasowej. W przypadku wybrania dwa woluminy, które należy toodifferent kontenery woluminów, umieszczania ich w jednym woluminie grupy, a następnie utwórz zasady tworzenia kopii zapasowej dla tej grupy woluminu każdego woluminu zostaną skopiowane nawet w kontenerze odpowiedni wolumin hello, przy użyciu odpowiedniego magazynu hello konto.

> [!NOTE]
> Wszystkie woluminy w grupie woluminu musi pochodzić od dostawcy usług w chmurze pojedynczego.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integracja z usługą kopiowania woluminów w tle systemu Windows
StorSimple Snapshot Manager używa hello danych spójnych z aplikacją toocapture usługi kopii tle (VSS) systemu Windows woluminu. VSS zapewnia spójność aplikacji komunikując się z obsługującym usługę VSS tworzenie aplikacji toocoordinate hello przyrostowe migawek. Usługa VSS zapewnia, że aplikacji hello są tymczasowo nieaktywne lub spoczynku, przy tworzeniu migawek woluminów. 

Witaj StorSimple Snapshot Manager wdrożenia usługi VSS współdziała z programu SQL Server i rodzajowy woluminów NTFS. Witaj proces przebiega następująco: 

1. Obiekt żądający, który jest zazwyczaj zarządzanie danymi i rozwiązanie do ochrony (takie jak StorSimple Snapshot Manager) lub aplikacji do tworzenia kopii zapasowej, wywołuje usługi VSS i żąda on toogather informacji z hello oprogramowania zapisywania w aplikacji docelowej hello.
2. Kontakty usługi VSS hello tooretrieve składnika zapisywania opis hello danych. Moduł zapisujący Hello zwraca hello opis hello toobe danych kopii zapasowej. 
3. Usługa VSS sygnalizuje aplikacja hello tooprepare hello edytora dla kopii zapasowej. Moduł zapisujący Hello przygotowuje hello danych do utworzenia kopii zapasowej, wykonując otwartych transakcji, aktualizowanie, dzienników transakcji i tak dalej, a następnie powiadamia VSS.
4. VSS powoduje, że moduł zapisujący hello danych aplikacji tootemporarily stop hello przechowuje i upewnij się, że żadne dane są zapisywane toohello woluminu podczas tworzenia kopii w tle hello. Ten krok zapewnia spójność danych i trwa nie dłużej niż 60 sekund.
5. VSS powoduje, że kopia hello toocreate hello dostawcy w tle. Dostawców, które mogą być oprogramowania - lub oparte na sprzęcie, zarządzanie hello woluminów, które są aktualnie uruchomione i utworzyć ich kopie w tle na żądanie. Dostawca Hello tworzy hello kopii w tle i powiadamia VSS po jego ukończeniu.
6. VSS kontaktów hello zapisywania toonotify hello aplikacja można wznowić operacji We/Wy i również tooconfirm, że We/Wy została pomyślnie wstrzymana w tle skopiuj tworzenia. 
7. Jeśli kopia hello zakończyło się pomyślnie, VSS zwraca hello obiektu żądającego toohello lokalizacji kopii. 
8. Jeśli dane zostały zapisane, gdy utworzono kopię w tle hello, to hello kopii zapasowej będą niespójne. VSS usuwa hello kopii w tle i powiadamia hello obiektu żądającego. Witaj obiektu żądającego można automatycznie Powtórz proces tworzenia kopii zapasowej hello lub powiadomić tooretry administratora hello go w późniejszym czasie.

Zobacz hello następującej ilustracji.

![Proces usługi VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Proces usługi kopiowania woluminów w tle systemu Windows** 

## <a name="backup-types-and-backup-policies"></a>Typy kopii zapasowych i zasady tworzenia kopii zapasowej
StorSimple Snapshot Manager można tworzyć kopie zapasowe danych i zapisać go lokalnie i w chmurze hello. Tooback StorSimple Snapshot Manager zapasową danych można użyć od razu lub służy do wykonywania kopii zapasowych automatycznie toocreate zasad tworzenia kopii zapasowej zgodnie z harmonogramem. Zasady tworzenia kopii zapasowej włączyć również toospecify ile migawki zostaną zachowane. 

### <a name="backup-types"></a>Typy kopii zapasowych
Program hello toocreate StorSimple Snapshot Manager następujące typy kopii zapasowych:

* **Migawki lokalne** — lokalne migawki są kopie danych woluminu, które są przechowywane na urządzeniu StorSimple hello punktu w czasie. Zazwyczaj ten typ kopii zapasowej można tworzyć i szybko przywrócić. Można użyć migawka lokalna, jak w przypadku lokalnej kopii zapasowej.
* **Migawki w chmurze** — w momencie kopii danych woluminu, które są przechowywane w chmurze hello są migawki w chmurze. Migawka w chmurze jest równoważna migawki tooa replikowane w systemie magazynu innych, poza nim. Migawki w chmurze są szczególnie przydatne w scenariuszach odzyskiwania po awarii.

### <a name="on-demand-and-scheduled-backups"></a>Na żądanie i zaplanowanych kopii zapasowych
StorSimple Snapshot Manager można zainicjować jednorazowe toobe kopii zapasowej natychmiast utworzenia lub skorzystać z tooschedule zasad tworzenia kopii zapasowej, cyklicznych operacji tworzenia kopii zapasowej.

Zasady tworzenia kopii zapasowej jest zestaw reguł automatycznego służy tooschedule regularnych kopii zapasowych. Zasady tworzenia kopii zapasowej pozwala toodefine hello częstotliwości i parametry tworzenie migawek woluminu określonej grupy. Zasady toospecify daty rozpoczęcia i wygaśnięcia, godziny, częstotliwości i wymagania dotyczące przechowywania, można użyć lokalnego i w chmurze migawki. Zasady są stosowane natychmiast po zdefiniowaniu. 

Można użyć tooconfigure StorSimple Snapshot Manager lub ponownie skonfigurować zasady tworzenia kopii zapasowej zawsze, gdy jest to konieczne. 

Należy skonfigurować hello następujących informacji dla każdej utworzonej zasady tworzenia kopii zapasowej:

* **Nazwa** — unikatowa nazwa hello hello wybrane zasady tworzenia kopii zapasowej.
* **Typ** — Witaj typ zasad tworzenia kopii zapasowej; migawka lokalna i migawka w chmurze.
* **Grupy woluminu** — przypisano hello woluminu grupy toowhich hello wybrane kopii zapasowej zasady.
* **Przechowywania** — Witaj liczba tooretain kopii zapasowych. Jeśli wybierzesz hello **wszystkie** okno, wszystkie kopie zapasowe są przechowywane do momentu osiągnięcia hello maksymalną liczbę kopii zapasowych na każdym woluminie, na które hello punktu zasad będzie zakończyć się niepowodzeniem i generuje komunikat o błędzie. Alternatywnie można określić liczbę kopii zapasowych tooretain (od 1 do 64).
* **Data** — Witaj Data utworzenia hello zasad tworzenia kopii zapasowej.

Informacji o konfigurowaniu zasad tworzenia kopii zapasowych, przejdź zbyt[toocreate Użyj StorSimple Snapshot Manager zasad tworzenia kopii zapasowych i zarządzanie nimi](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Zadanie tworzenia kopii zapasowej, monitorowanie i zarządzanie
Można użyć hello toomonitor StorSimple Snapshot Manager i zarządzanie nadchodzących, zaplanowane i zakończonych zadań tworzenia kopii zapasowej. Ponadto StorSimple Snapshot Manager udostępnia katalog się too64 ukończyć tworzenia kopii zapasowych. Można użyć toofind katalogu hello i Przywracanie woluminów lub poszczególnych plików. 

Informacje o monitorowaniu zadań tworzenia kopii zapasowej, przejdź zbyt[tooview Użyj StorSimple Snapshot Manager zadania tworzenia kopii zapasowej i zarządzać nimi](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [za pomocą programu StorSimple Snapshot Manager tooadminister rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Pobierz [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220).

