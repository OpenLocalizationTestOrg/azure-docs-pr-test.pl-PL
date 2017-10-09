---
title: informacje o wersji aaaStorSimple wirtualnego tablicy | Dokumentacja firmy Microsoft
description: "Opisuje krytyczne Otwórz problemy i rozwiązania dla hello tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>Informacje o wersji tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji zidentyfikować hello krytyczne problemy otwarte dla wersji ogólnodostępnej (GA) marca 2016 hello hello Microsoft Azure StorSimple wirtualnego tablicy (znany także jako urządzenia wirtualnego StorSimple na lokalne powitania lub hello wirtualnego StorSimple urządzenia). Ta wersja odpowiada wersji toosoftware 10.0.10271.0.

informacje o wersji Hello jest stale aktualizowany, a wykrywane krytyczne problemy wymagające obejścia są dodawane. Przed wdrożeniem urządzenia wirtualnego StorSimple, należy dokładnie przejrzeć hello informacje zawarte w hello informacje o wersji. 

Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Obejście/komentarzy |
| --- | --- | --- | --- |
| **1.** |Aktualizacje |Witaj urządzenia wirtualne utworzone w wersji zapoznawczej hello nie może być zaktualizowane tooa obsługiwane ogólnodostępnej wersji. |Te urządzenia wirtualnego musi być nie powiodło się za pośrednictwem hello wersji ogólnodostępnej za pomocą przepływu pracy (DR) odzyskiwania po awarii. |
| **2.** |Dysk z danymi udostępnione |Po uprzednim udostępnieniu dysku danych o określonym rozmiarze określonym i utworzyć odpowiednie urządzenie wirtualne hello StorSimple, użytkownik musi nie zwiększania lub zmniejszania hello dysku danych. Dlatego próba toodo spowoduje utratę wszystkich hello danych w warstwach lokalne powitania hello urządzenia. | |
| **3.** |Zasady grupy |Gdy urządzenie jest przyłączony do domeny, stosowanie zasad grupy może niekorzystnie wpłynąć na powitania operacji urządzenia. |Sprawdź, czy tablica wirtualnej jest w jego własnej jednostce organizacyjnej (OU) dla usługi Active Directory i żadne obiekty zasad grupy (GPO) są stosowane tooit. |
| **4.** |Lokalnego interfejsu użytkownika sieci web |Ulepszone funkcje zabezpieczeń są włączone w programie Internet Explorer (nazywana konfiguracją IE ESC), niektórych lokalnego interfejsu użytkownika strony, takich jak rozwiązywanie problemów lub konserwacji może nie działać poprawnie. Przyciski na tych stronach również mogą nie działać. |Wyłącz funkcje zwiększonych zabezpieczeń programu Internet Explorer. |
| **5.** |Lokalnego interfejsu użytkownika sieci web |Na maszynie wirtualnej funkcji Hyper-V hello interfejsy sieciowe w sieci web hello interfejsu użytkownika są wyświetlane jako 10 GB/s interfejsów. |To zachowanie jest odbicia funkcji Hyper-v. Funkcji Hyper-V jest zawsze zawiera 10 GB/s dla wirtualnych kart sieciowych. |
| **6.** |Woluminy warstwowe lub udziały |Blokowanie dla aplikacji, które współpracują z hello StorSimple woluminy warstwowe zakresu bajtów nie jest obsługiwane. Jeśli jest włączone blokowanie zakresu bajtów, Obsługa poziomów StorSimple nie będzie działać. |Zalecane środki obejmują: <br></br>Wyłącz zakresu bajtów blokowania w logiki aplikacji.<br></br>Wybierz dane tooput dla tej aplikacji woluminów przypiętych lokalnie nazwą tootiered woluminów.<br></br>*Zastrzeżenie:*: Jeśli za pomocą lokalnie przypięty woluminów i jest włączone blokowanie zakresu bajtów, należy pamiętać, wolumin przypięty lokalnie hello można online nawet przed hello Przywracanie zostało ukończone. W takich przypadkach jeśli przywracania jest w toku, następnie należy poczekać hello toocomplete przywracania. |
| **7.** |Udziały warstwowych |Praca z dużych plików może spowodować wolne warstwy w poziomie. |Podczas pracy z dużymi plikami, zaleca się czy plik największy hello jest mniejszy niż rozmiar udziału hello % 3. |
| **8.** |Używane pojemności dla akcji |Może zostać wyświetlony udostępnianie zużycie hello braku żadnych danych w udziale hello. Jest to spowodowane pojemność hello używane w przypadku udziałów obejmuje metadanych. | |
| **9.** |Odzyskiwanie po awarii |Odzyskiwanie po awarii hello toohello serwera plików można wykonać tylko tej samej domeny co hello urządzenia źródłowego. Urządzenie docelowe tooa odzyskiwania po awarii w innej domenie nie jest obsługiwane w tej wersji. |To są realizowane w nowszej wersji. |
| **10.** |Azure PowerShell |urządzenia wirtualnego StorSimple Hello nie można zarządzać za pomocą hello Azure PowerShell w tej wersji. |Całe Zarządzanie hello hello urządzeń wirtualnych powinna być wykonywana za pośrednictwem hello klasycznego portalu Azure i lokalne powitania interfejsu użytkownika sieci web. |
| **11.** |Zmienianie hasła |konsoli urządzenia wirtualnego tablicy Hello akceptuje tylko dane wejściowe w formacie klawiatury en US. | |
| **12.** |PROTOKOŁU CHAP |Nie można usunąć poświadczenia CHAP raz utworzony. Ponadto zmodyfikowanie hello CHAP poświadczenia należy tootake hello woluminy w trybie offline, a następnie przełączyć je w trybie online dla efektu tootake zmiany hello. |Te zostaną rozwiązane w nowszej wersji. |
| **13.** |Serwer iSCSI |Witaj, "Użyto magazynu" wyświetlany dla woluminu iSCSI mogą być różne w hello usługi Menedżer StorSimple i hello iSCSI hosta. |hosta iSCSI Hello ma hello widok systemu plików.<br></br>urządzenie Hello widzi bloki hello przydzielone, gdy wolumin hello na powitania maksymalny rozmiar. |

