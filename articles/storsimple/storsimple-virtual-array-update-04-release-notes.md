---
title: informacje o wersji 0,4 wirtualnego Update tablicy aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje Otwórz krytyczne problemy i rozwiązania dotyczące uruchamiania tablicy wirtualnego StorSimple hello 0,4 aktualizacji."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>Informacje o wersji 0,4 Update tablicy z wirtualnego StorSimple

## <a name="overview"></a>Omówienie

Witaj poniższych informacjach o wersji zidentyfikować hello krytyczne problemy otwarte i hello rozwiązane problemy dotyczące aktualizacji tablicy wirtualne Microsoft Azure StorSimple.

informacje o wersji Hello jest stale aktualizowany, a wykrywane krytyczne problemy wymagające obejścia są dodawane. Przed wdrożeniem tablica wirtualnego StorSimple, należy dokładnie przejrzeć hello informacje zawarte w hello informacje o wersji.

Aktualizacja 0,4 odpowiada wersji oprogramowania toohello **10.0.10289.0**.

> [!NOTE]
> Aktualizacje są one i ponownym uruchomieniu urządzenia. Jeśli we/wy jest w toku, urządzenia hello wiąże przestoju.


## <a name="whats-new-in-hello-update-04"></a>Nowości w aktualizacji 0,4 hello
Aktualizacja 0,4 jest głównie kompilacji Poprawka usterki sprzężona kilka ulepszeń. W tej wersji kilka błędów, co spowoduje niepowodzenie wykonywania kopii zapasowej w poprzedniej wersji hello zostały rozwiązane. Hello głównych ulepszeń i poprawek usterek są następujące:

- **Wykonaj kopię zapasową usprawnień wydajności** -tej wersji wprowadził kilka kluczowych usprawnień wydajności tworzenia kopii zapasowych hello tooimprove. W związku z tym hello kopii zapasowych, obejmujących wiele plików Zobacz znaczny spadek hello toocomplete czasu, aby uzyskać pełne i przyrostowe kopie zapasowe.

- **Lepszą wydajnością przywracania** — ta wersja zawiera ulepszenia, które znacznie poprawić wydajność przywracania hello, korzystając z dużej liczby plików. Przy użyciu 2-4 miliony plików, firma Microsoft zaleca obsługi administracyjnej wirtualnego tablicy o wielkości 16 GB pamięci RAM toosee hello ulepszenia. Gdy przy użyciu mniejszej niż 2 miliony plików i hello minimalne wymagania dla maszyny wirtualnej hello kontynuuje toobe 8 GB pamięci RAM.

- **Ulepszenia tooSupport pakietu** -hello ulepszenia rejestrowania hello statystyki dla dysku, Procesora, pamięci, sieci i chmury do pakietu obsługi hello zwiększając proces hello diagnozowania/debugowanie problemów z urządzeniami.

- **ISCSI woluminów too200 GB przypięty lokalnie limit** — dla woluminów przypiętych lokalnie, zalecamy ograniczenie tooa 200 GB iSCSI woluminu w macierzy wirtualnego StorSimple. Hello lokalnego rezerwacji woluminy warstwowe nadal toobe 10% hello elastycznie rozmiar woluminu, ale jest ograniczona do 200 GB. 

- **Poprawki błędów związanych z kopii zapasowej** — w poprzednich wersjach oprogramowania, zostały powiązane toobackups problemy, które mogłyby spowodować niepowodzenie wykonywania kopii zapasowej. Te błędy rozwiązano w tej wersji.


## <a name="issues-fixed-in-hello-update-04"></a>Problemy rozwiązane w hello aktualizacji 0,4

Witaj Poniższa tabela zawiera podsumowanie problemy rozwiązane w tej wersji.

| Nie. | Funkcja | Problem |
| --- | --- | --- |
| 1 |Wydajność tworzenia kopii zapasowej|W hello wcześniejszych wersjach, hello kopie zapasowe obejmujące wiele plików zajmie toocomplete długi czas (w kolejności hello dni). W tej wersji zarówno hello pełne i przyrostowe kopie zapasowe Zobacz znaczny spadek hello toocompletion czasu. |
| 2 |Pakiet pomocy technicznej|Dzienniki pomocy technicznej toohello wprowadzania hello obsługi pakietów bardzo efektywnym sposobem, w dowolnym rozwiązywania problemów z urządzeniami teraz zalogowany dysku, Procesora, pamięci, sieci i statystyki chmury.|
| 3 |Tworzenie kopii zapasowych |We wcześniejszych wersjach długotrwałą kopii zapasowych może spowodować brak miejsca na urządzeniu hello, co spowoduje niepowodzenie wykonywania kopii zapasowej. Ta usterka zostanie rozwiązana w tej wersji, zezwalając tooqueue kopii zapasowych nie więcej niż 5 w tym samym czasie.|
| 4 |iSCSI | We wcześniejszych wersjach hello rezerwacji lokalnych woluminów warstwowych lub przypięty lokalnie był 10% hello elastycznie rozmiar woluminu. W tej wersji rezerwacji lokalne powitania wszystkie woluminy iSCSI (lokalnie przypięty lub do warstwy) jest ograniczona too10% składającą się maksymalnie z maksymalnie 200 GB (dla woluminów warstwowych większych niż 2 TB) tym samym zwalnianie więcej miejsca na dysku lokalnym hello. Zaleca się woluminów hello przypięty lokalnie w tej wersji ograniczone too200 GB.|


## <a name="known-issues-in-hello-update-04"></a>Znane problemy w hello aktualizacji 0,4

Hello Poniższa tabela zawiera podsumowanie znane problemy dla hello tablicy wirtualnego StorSimple oraz problemy hello wersji inaczej niż w poprzednich wydaniach hello. 

| Nie. | Funkcja | Problem | Obejście/komentarzy |
| --- | --- | --- | --- |
| **1.** |Aktualizacje |Witaj urządzenia wirtualne utworzone w wersji zapoznawczej hello nie może być zaktualizowane tooa obsługiwane ogólnodostępnej wersji. |Te urządzenia wirtualnego musi być nie powiodło się za pośrednictwem hello wersji ogólnodostępnej za pomocą przepływu pracy (DR) odzyskiwania po awarii. |
| **2.** |Dysk z danymi udostępnione |Po uprzednim udostępnieniu dysku danych o określonym rozmiarze określonym i utworzyć odpowiednie urządzenie wirtualne hello StorSimple, użytkownik musi nie zwiększania lub zmniejszania hello dysku danych. Próba wyniki toodo doprowadzi do utraty wszystkich hello danych w warstwach lokalne powitania hello urządzenia. | |
| **3.** |Zasady grupy |Gdy urządzenie jest przyłączony do domeny, stosowanie zasad grupy może niekorzystnie wpłynąć na powitania operacji urządzenia. |Sprawdź, czy tablica wirtualnej jest w jego własnej jednostce organizacyjnej (OU) dla usługi Active Directory i żadne obiekty zasad grupy (GPO) są stosowane tooit. |
| **4.** |Lokalnego interfejsu użytkownika sieci web |Ulepszone funkcje zabezpieczeń są włączone w programie Internet Explorer (nazywana konfiguracją IE ESC), niektórych lokalnego interfejsu użytkownika strony, takich jak rozwiązywanie problemów lub konserwacji może nie działać poprawnie. Przyciski na tych stronach również mogą nie działać. |Wyłącz funkcje zwiększonych zabezpieczeń programu Internet Explorer. |
| **5.** |Lokalnego interfejsu użytkownika sieci web |Na maszynie wirtualnej funkcji Hyper-V hello interfejsy sieciowe w sieci web hello interfejsu użytkownika są wyświetlane jako 10 GB/s interfejsów. |To zachowanie jest odbicia funkcji Hyper-v. Funkcji Hyper-V jest zawsze zawiera 10 GB/s dla wirtualnych kart sieciowych. |
| **6.** |Woluminy warstwowe lub udziały |Blokowanie dla aplikacji, które współpracują z hello StorSimple woluminy warstwowe zakresu bajtów nie jest obsługiwane. Jeśli jest włączone blokowanie zakresu bajtów, Obsługa poziomów StorSimple nie działa. |Zalecane środki obejmują: <br></br>Wyłącz zakresu bajtów blokowania w logiki aplikacji.<br></br>Wybierz dane tooput dla tej aplikacji woluminów przypiętych lokalnie nazwą tootiered woluminów.<br></br>*Zastrzeżenie:*: gdy lokalnie przy użyciu przypięty woluminów i jest włączone blokowanie zakresu bajtów, wolumin przypięty lokalnie hello może być online nawet przed hello Przywracanie zostało ukończone. W takich przypadkach jeśli przywracania jest w toku, następnie należy poczekać hello toocomplete przywracania. |
| **7.** |Udziały warstwowych |Praca z dużych plików może spowodować wolne warstwy w poziomie. |Podczas pracy z dużymi plikami, zaleca się czy plik największy hello jest mniejszy niż rozmiar udziału hello % 3. |
| **8.** |Używane pojemności dla akcji |Może zostać wyświetlony udostępnianie zużycia, gdy nie ma żadnych danych w udziale hello. Jest to spowodowane pojemność hello używane w przypadku udziałów obejmuje metadanych. | |
| **9.** |Odzyskiwanie po awarii |Odzyskiwanie po awarii hello toohello serwera plików można wykonać tylko tej samej domeny co hello urządzenia źródłowego. Urządzenie docelowe tooa odzyskiwania po awarii w innej domenie nie jest obsługiwane w tej wersji. |Ten sposób jest implementowany w nowszej wersji. |
| **10.** |Azure PowerShell |urządzenia wirtualnego StorSimple Hello nie można zarządzać za pomocą hello Azure PowerShell w tej wersji. |Całe Zarządzanie hello hello urządzeń wirtualnych powinna być wykonywana za pośrednictwem hello klasycznego portalu Azure i lokalne powitania interfejsu użytkownika sieci web. |
| **11.** |Zmienianie hasła |konsoli urządzenia wirtualnego tablicy Hello akceptuje tylko dane wejściowe w formacie klawiatury en US. | |
| **12.** |PROTOKOŁU CHAP |Nie można usunąć poświadczenia CHAP raz utworzony. Ponadto zmodyfikowanie hello CHAP poświadczenia muszą tootake hello woluminy w trybie offline i przenieść je w trybie online dla efektu tootake zmiany hello. |Ten problem został rozwiązany w nowszej wersji. |
| **13.** |Serwer iSCSI |Witaj, "Użyto magazynu" wyświetlany dla woluminu iSCSI mogą być różne w hello usługi Menedżer StorSimple i hello iSCSI hosta. |hosta iSCSI Hello ma hello widok systemu plików.<br></br>urządzenie Hello widzi bloki hello przydzielone, gdy wolumin hello na powitania maksymalny rozmiar. |
| **14.** |Serwer plików |Jeśli plik w folderze alternatywnych danych strumienia (AD) skojarzonych z nim, hello REKLAM nie jest kopię zapasową lub przywrócić za pomocą odzyskiwania po awarii, powielania i odzyskiwanie na poziomie elementu. | |
| **15.** |Serwer plików |Łącza symbolicznego nie są obsługiwane. | |
| **16.** |Serwer plików |Pliki chronione przez Windows System szyfrowania plików (EFS) po skopiowaniu za pośrednictwem lub przechowywane na powitania wynik serwera plików tablicy wirtualnego StorSimple w nieobsługiwanej konfiguracji.  | |

## <a name="next-step"></a>Następny krok
[Zainstaluj aktualizację 0,4](storsimple-virtual-array-install-update-04.md) na tablica wirtualne StorSimple.

## <a name="references"></a>Dokumentacja
Szukasz starsze Uwaga wersji? Przejdź do strony: 

* [Informacje o wersji 0,3 aktualizacji tablicy wirtualnego StorSimple](storsimple-ova-update-03-release-notes.md)
* [Informacje o wersji aktualizacji tablicy wirtualnego StorSimple 0,1 i 0,2](storsimple-ova-update-01-release-notes.md)
* [Informacje o wersji dostępności ogólne tablicy wirtualnego StorSimple](storsimple-ova-pp-release-notes.md)

