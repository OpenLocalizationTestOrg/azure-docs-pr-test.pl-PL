---
title: informacje o wersji aaaStorSimple wirtualnego aktualizacje tablicy | Dokumentacja firmy Microsoft
description: "Opisuje Otwórz krytyczne problemy i rozwiązania dotyczące uruchamiania tablicy wirtualnego StorSimple hello 0,3 aktualizacji."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>Informacje o wersji 0,3 Update tablicy z wirtualnego StorSimple
## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji zidentyfikować hello krytyczne problemy otwarte i hello rozwiązane problemy dotyczące aktualizacji tablicy wirtualne Microsoft Azure StorSimple.

informacje o wersji Hello jest stale aktualizowany, a wykrywane krytyczne problemy wymagające obejścia są dodawane. Przed wdrożeniem tablica wirtualnego StorSimple, należy dokładnie przejrzeć hello informacje zawarte w hello informacje o wersji.

Update 0.3 odpowiada wersji oprogramowania toohello **10.0.10288.0**.

> [!NOTE]
> Aktualizacje są one i ponownym uruchomieniu urządzenia. Jeśli we/wy jest w toku, urządzenia hello wiąże przestoju.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>What's new in hello Update 0.3
Update 0.3 jest głównie poprawka błędu kompilacji. W tej wersji kilka błędów, co spowoduje niepowodzenie wykonywania kopii zapasowej w poprzedniej wersji hello zostały rozwiązane.

## <a name="issues-fixed-in-hello-update-03"></a>Problemy rozwiązane w hello Update 0.3
Witaj Poniższa tabela zawiera podsumowanie problemy rozwiązane w tej wersji.

| Nie. | Funkcja | Problem |
| --- | --- | --- |
| 1 |Tworzenie kopii zapasowych |Wystąpił problem w hello wcześniejszą wersją, których kopie zapasowe hello spowoduje niepowodzenie toocomplete udziału plików. Jeśli ten problem wystąpił, hello zadanie tworzenia kopii zapasowej nie powiedzie się i zgłoszono alert krytyczny na powitania — użytkownik hello toonotify usługi Menedżer StorSimple. Ten problem nie wpływają na powitania dane w udziałach hello ani uzyskać dostęp do danych toohello. Witaj główną przyczynę został zidentyfikowaniu i usunięciu w tej wersji. <br></br> poprawka Hello nie ma zastosowania wstecznie tooshares, który jest już wyświetlany ten problem. Klienci, którzy są występuje ten problem należy najpierw zastosować Update 0.3, a następnie skontaktuj się z Microsoft Support tooperform problemem hello toofix kopii zapasowej całego systemu. Zamiast kontaktowania się z Microsoft Support, klientów można także przywrócić tooa nowy udział z dobrej kopii zapasowej udziałów hello, których to dotyczy. |
| 2 |iSCSI |Wystąpił problem w hello wcześniejszych wersji, gdzie woluminów hello zniknie podczas kopiowania danych tooa woluminu na powitania tablicy wirtualnego StorSimple. Ten problem został rozwiązany w tej wersji. <br></br> Hello poprawki zostały zastosowane tylko na nowo utworzony woluminów. poprawki Hello nie należy stosować wstecznie toovolumes, który jest już wyświetlany ten problem. Klienci zalecana woluminy hello wpływ toobring online za pośrednictwem hello klasycznego portalu Azure, wykonaj kopię zapasową dla tych woluminów, a następnie przywróć te woluminy toonew woluminy. |

## <a name="known-issues-in-hello-update-03"></a>Znane problemy w hello Update 0.3
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

## <a name="next-step"></a>Następny krok
[Zainstaluj aktualizację 0,3](storsimple-ova-install-update-01.md) na tablica wirtualne StorSimple.

## <a name="references"></a>Dokumentacja
Szukasz starsze Uwaga wersji? Przejdź do strony: 

* [Informacje o wersji aktualizacji tablicy wirtualnego StorSimple 0,1 i 0,2](storsimple-ova-update-01-release-notes.md)
* [Informacje o wersji dostępności ogólne tablicy wirtualnego StorSimple](storsimple-ova-pp-release-notes.md)

