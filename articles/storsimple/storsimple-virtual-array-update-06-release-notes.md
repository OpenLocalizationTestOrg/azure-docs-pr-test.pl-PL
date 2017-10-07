---
title: informacje o wersji 0,6 wirtualnego Update tablicy aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje Otwórz krytyczne problemy i rozwiązania dotyczące uruchamiania tablicy wirtualnego StorSimple hello 0,6 aktualizacji."
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
ms.date: 05/24/2017
ms.author: alkohli
ms.openlocfilehash: 7b573457dc07ce41e95d49d66ccc174045f31a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-06-release-notes"></a>Informacje o wersji 0,6 Update tablicy z wirtualnego StorSimple

## <a name="overview"></a>Omówienie

Witaj poniższych informacjach o wersji zidentyfikować hello krytyczne problemy otwarte i hello rozwiązane problemy dotyczące aktualizacji tablicy wirtualne Microsoft Azure StorSimple.

informacje o wersji Hello jest stale aktualizowany, a wykrywane krytyczne problemy wymagające obejścia są dodawane. Przed wdrożeniem tablica wirtualnego StorSimple, należy dokładnie przejrzeć hello informacje zawarte w hello informacje o wersji.

Aktualizacja 0,6 odpowiada wersji oprogramowania toohello **10.0.10293.0**.

> [!IMPORTANT]
> - Aktualizacje są one i ponownym uruchomieniu urządzenia. Jeśli we/wy jest w toku, urządzenia hello wiąże przestoju. Szczegółowe informacje dotyczące sposobu tooapply hello aktualizacji, przejdź zbyt[instalacji aktualizacji 0,6](storsimple-virtual-array-install-update-06.md).
>
> - Zdecydowanie zaleca się zainstalowanie aktualizacji 0,6 natychmiast, ponieważ zawiera on poprawki błędów krytycznych.


## <a name="whats-new-in-hello-update-06"></a>What's new in hello aktualizacji 0,6
Aktualizacja 0,6 jest aktualizacji krytycznych i powinny być wdrażane bezpośrednio. Ta aktualizacja zawiera hello następujące poprawki: 

- **Poprawki zabezpieczeń systemu Windows** — to wydanie zawiera **poprawki zabezpieczenia krytyczne systemu Windows**. Przejrzyj następujące aktualizacje zabezpieczeń, aby uzyskać więcej informacji na temat problemów z zabezpieczeniami hello hello i hello skojarzone poprawki:
    - [Grudnia 2016 jakości tylko zabezpieczeń aktualizacji dla Windows 8.1 i Windows Server 2012 R2](https://support.microsoft.com/help/3205400/december-2016-security-only-quality-update-for-windows-8.1-and-windows-server-2012-r2)
    - [2017 marca zabezpieczeń, jakości tylko aktualizacji dla Windows 8.1 i Windows Server 2012 R2](https://support.microsoft.com/help/4012213/march-2017-security-only-quality-update-for-windows-8-1-and-windows-server-2012-r23)
    - [9 maja 2017 — KB4019213 (tylko do zabezpieczeń aktualizacja)](https://support.microsoft.com/help/4019213/windows-8-update-kb4019213)

- **Przywróć poprawka** -we wcześniejszych wersjach został usterki, które mogłyby uniemożliwiać przywracania hello ukończenie. Ten problem został rozwiązany w tej wersji.


## <a name="issues-fixed-in-hello-update-06"></a>Problemy rozwiązane w hello aktualizacji 0,6

Witaj Poniższa tabela zawiera podsumowanie problemy rozwiązane w tej wersji.

| Nie. | Funkcja | Problem |
| --- | --- | --- |
| 1 |Bezpieczeństwo| Ta wersja zawiera aktualizacje krytyczne zabezpieczenia systemu Windows. Zalecamy natychmiastowe zainstalowanie tej aktualizacji.|
| 2 |Przywracanie| Podczas przywracania wystąpił sytuacji wyścigu, które mogłyby uniemożliwiać zadanie przywracania hello zakończenie działania. Poprawka błędu Hello adresów sytuacja wyścigu.|


## <a name="known-issues-in-hello-update-06"></a>Znane problemy w hello aktualizacji 0,6

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
| **8.** |Używane pojemności dla akcji |Może zostać wyświetlony udostępnianie zużycia, gdy nie ma żadnych danych w udziale hello. To zużycie jest ponieważ pojemność hello używane w przypadku udziałów obejmuje metadanych. | |
| **9.** |Odzyskiwanie po awarii |Odzyskiwanie po awarii hello toohello serwera plików można wykonać tylko tej samej domeny co hello urządzenia źródłowego. Urządzenie docelowe tooa odzyskiwania po awarii w innej domenie nie jest obsługiwane w tej wersji. |Ten sposób jest implementowany w nowszej wersji. Aby uzyskać więcej informacji, przejdź zbyt[trybu Failover i odzyskiwania po awarii dla macierzy wirtualnego StorSimple](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |urządzenia wirtualnego StorSimple Hello nie można zarządzać za pomocą hello Azure PowerShell w tej wersji. |Całe Zarządzanie hello hello urządzeń wirtualnych z ma się odbywać za pośrednictwem hello Azure portal i hello lokalnego interfejsu użytkownika sieci web. |
| **11.** |Zmienianie hasła |Hello konsoli urządzenia wirtualnego tablicy akceptuje tylko danych wejściowych w en-us klawiatury formatu. | |
| **12.** |PROTOKOŁU CHAP |Nie można usunąć poświadczenia CHAP raz utworzony. Ponadto zmodyfikowanie hello CHAP poświadczenia muszą tootake hello woluminy w trybie offline i przenieść je w trybie online dla efektu tootake zmiany hello. |Ten problem został rozwiązany w nowszej wersji. |
| **13.** |Serwer iSCSI |Witaj, "Użyto magazynu" wyświetlany dla woluminu iSCSI mogą być różne w hello usługi Menedżer urządzenia StorSimple i hello iSCSI hosta. |hosta iSCSI Hello ma hello widok systemu plików.<br></br>urządzenie Hello widzi bloki hello przydzielone, gdy wolumin hello na powitania maksymalny rozmiar. |
| **14.** |Serwer plików |Jeśli plik w folderze alternatywnych danych strumienia (AD) skojarzonych z nim, hello REKLAM nie jest kopię zapasową lub przywrócić za pomocą odzyskiwania po awarii, powielania i odzyskiwanie na poziomie elementu. | |
| **15.** |Serwer plików |Łącza symbolicznego nie są obsługiwane. | |
| **16.** |Serwer plików |Pliki chronione przez Windows System szyfrowania plików (EFS) po skopiowaniu za pośrednictwem lub przechowywane na powitania wynik serwera plików tablicy wirtualnego StorSimple w nieobsługiwanej konfiguracji.  | |
| **17.** |Aktualizacje |Jeśli zostanie wyświetlony błąd kodu: 2359302 (szesnastkowo 0x240006) podczas próby tooinstall poprawek za pomocą hello lokalnego interfejsu użytkownika, a następnie to oznacza, że ta poprawka hello jest już zainstalowana na urządzeniu.   | |

## <a name="next-step"></a>Następny krok
[Zainstaluj aktualizację 0,6](storsimple-virtual-array-install-update-06.md) na tablica wirtualne StorSimple.

## <a name="references"></a>Dokumentacja
Szukasz starsze Uwaga wersji? Przejdź do strony:

* [Informacje o wersji 0,5 aktualizacji tablicy wirtualnego StorSimple](storsimple-virtual-array-update-05-release-notes.md)
* [Informacje o wersji 0,4 aktualizacji tablicy wirtualnego StorSimple](storsimple-virtual-array-update-04-release-notes.md)
* [Informacje o wersji 0,3 aktualizacji tablicy wirtualnego StorSimple](storsimple-ova-update-03-release-notes.md)
* [Informacje o wersji aktualizacji tablicy wirtualnego StorSimple 0,1 i 0,2](storsimple-ova-update-01-release-notes.md)
* [Informacje o wersji dostępności ogólne tablicy wirtualnego StorSimple](storsimple-ova-pp-release-notes.md)

