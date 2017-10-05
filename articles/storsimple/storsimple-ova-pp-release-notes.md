---
title: Informacje o wersji tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Opisuje krytyczne Otwórz problemy i rozwiązania dla tablicy wirtualne StorSimple."
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
ms.openlocfilehash: f3ea83e32af4de2637d12766ee8c51adfbf0d3a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>Informacje o wersji tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie
W poniższych informacjach o zidentyfikować krytyczne problemy otwarte w wersji ogólnodostępnej (GA) marca 2016 Microsoft Azure StorSimple wirtualnego tablicy (znanej także jako urządzenie wirtualne StorSimple lokalnymi lub urządzenie wirtualne StorSimple). Ta wersja odpowiada wersji oprogramowania 10.0.10271.0.

Informacje o wersji są stale aktualizowane i wykrywane krytyczne problemy wymagające obejścia są dodawane. Przed wdrożeniem urządzenia wirtualnego StorSimple, należy dokładnie przejrzeć informacje zawarte w informacjach o wersji. 

Poniższa tabela zawiera podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Obejście/komentarzy |
| --- | --- | --- | --- |
| **1.** |Aktualizacje |Nie można zaktualizować urządzenia wirtualne utworzone w wersji zapoznawczej do obsługiwanej wersji ogólnej dostępności. |Te urządzenia wirtualnego należy można przełączyć w wersji ogólnodostępnej za pomocą przepływu pracy (DR) odzyskiwania po awarii. |
| **2.** |Dysk z danymi udostępnione |Po aprowizowaniu dysk z danymi o określonym rozmiarze określonym i utworzyć odpowiednie urządzenia wirtualnego StorSimple, użytkownik musi nie zwiększania lub zmniejszania dysk z danymi. Takie próby spowoduje utratę wszystkich danych w warstwach lokalnych urządzenia. | |
| **3.** |Zasady grupy |Gdy urządzenie jest przyłączony do domeny, stosowanie zasad grupy może niekorzystnie wpłynąć na działanie urządzenia. |Sprawdź, czy tablica wirtualnej jest w jego własnej jednostce organizacyjnej (OU) usługi Active Directory i żadne obiekty zasad grupy (GPO) są stosowane do niego. |
| **4.** |Lokalnego interfejsu użytkownika sieci web |Ulepszone funkcje zabezpieczeń są włączone w programie Internet Explorer (nazywana konfiguracją IE ESC), niektórych lokalnego interfejsu użytkownika strony, takich jak rozwiązywanie problemów lub konserwacji może nie działać poprawnie. Przyciski na tych stronach również mogą nie działać. |Wyłącz funkcje zwiększonych zabezpieczeń programu Internet Explorer. |
| **5.** |Lokalnego interfejsu użytkownika sieci web |Na maszynie wirtualnej funkcji Hyper-V interfejsy sieciowe w sieci web interfejsu użytkownika są wyświetlane jako 10 GB/s interfejsów. |To zachowanie jest odbicia funkcji Hyper-v. Funkcji Hyper-V jest zawsze zawiera 10 GB/s dla wirtualnych kart sieciowych. |
| **6.** |Woluminy warstwowe lub udziały |Zakres bajtów blokady aplikacji współdziałających ze StorSimple woluminy warstwowe nie jest obsługiwane. Jeśli jest włączone blokowanie zakresu bajtów, Obsługa poziomów StorSimple nie będzie działać. |Zalecane środki obejmują: <br></br>Wyłącz zakresu bajtów blokowania w logiki aplikacji.<br></br>Wybierz, aby umieścić dane dla tej aplikacji w woluminów przypiętych lokalnie, zamiast woluminy warstwowe.<br></br>*Zastrzeżenie:*: w przypadku lokalnie przy użyciu przypięty woluminów i jest włączone blokowanie zakresu bajtów, należy pamiętać, że woluminu przypiętego lokalnie może być w trybie online nawet przed zakończeniem przywracania. W takich przypadkach jeśli przywracania jest w toku, następnie należy poczekać na ukończenie przywracania. |
| **7.** |Udziały warstwowych |Praca z dużych plików może spowodować wolne warstwy w poziomie. |Podczas pracy z dużymi plikami, zaleca się, że największy plik jest mniejszy niż rozmiar udziału % 3. |
| **8.** |Używane pojemności dla akcji |Może zostać wyświetlony udostępnianie użycie w przypadku braku żadnych danych w udziale. Jest to spowodowane pojemność używane udziały obejmuje metadanych. | |
| **9.** |Odzyskiwanie po awarii |Może wyłącznie wykonywać odzyskiwanie po awarii, serwera plików do tej samej domeny co urządzenia źródłowego. Odzyskiwanie po awarii do urządzenia docelowego w innej domenie nie jest obsługiwane w tej wersji. |To są realizowane w nowszej wersji. |
| **10.** |Azure PowerShell |Urządzenia wirtualne StorSimple nie można zarządzać za pomocą programu Azure PowerShell w tej wersji. |Zarządzanie urządzeń wirtualnych powinna być wykonywana za pośrednictwem klasycznego portalu Azure i lokalnego interfejsu użytkownika sieci web. |
| **11.** |Zmienianie hasła |Konsoli urządzenia wirtualnego tablicy akceptuje tylko dane wejściowe w formacie klawiatury en US. | |
| **12.** |PROTOKOŁU CHAP |Nie można usunąć poświadczenia CHAP raz utworzony. Ponadto Jeśli zmodyfikujesz poświadczeń protokołu CHAP, konieczne będzie woluminy Przełącz do trybu offline, a następnie przełączyć je na online, aby zmiany zaczęły obowiązywać. |Te zostaną rozwiązane w nowszej wersji. |
| **13.** |Serwer iSCSI |"Użyto magazynu" wyświetlany dla woluminu iSCSI mogą się różnić w usługi Menedżer StorSimple i hosta iSCSI. |Hosta iSCSI ma widok systemu plików.<br></br>Urządzenie widzi bloki przydzielone, gdy wolumin w maksymalnym rozmiarze. |

