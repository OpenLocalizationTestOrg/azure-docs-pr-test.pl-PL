---
title: informacje o wersji aaaStorSimple wirtualnego aktualizacje tablicy | Dokumentacja firmy Microsoft
description: "Opisuje krytyczne Otwórz problemy i rozwiązania dla hello tablicy wirtualnego StorSimple uruchomieniu Update 0.2 i 0,1."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Informacje o wersji wirtualnej tablicy Update 0.2 i 0,1 StorSimple
## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji zidentyfikować hello krytyczne problemy otwarte i hello rozwiązane problemy dotyczące aktualizacji tablicy wirtualne Microsoft Azure StorSimple. (Microsoft Azure StorSimple wirtualnego tablicy jest znanej także jako urządzenie wirtualne hello StorSimple lokalnymi lub hello urządzenia wirtualnego StorSimple). 

informacje o wersji Hello jest stale aktualizowany, a wykrywane krytyczne problemy wymagające obejścia są dodawane. Przed wdrożeniem urządzenia wirtualnego StorSimple, należy dokładnie przejrzeć hello informacje zawarte w hello informacje o wersji.

Update 0.2 odpowiada wersji oprogramowania toohello **10.0.10280.0**; Wersja jest aktualizacja 0,1 **10.0.10279.0**. Poniższe rozdziały zawierają Hello Lista zmian hello każdej aktualizacji. 

> [!NOTE]
> Aktualizacje są one i zostanie ponownie uruchomić urządzenie. Jeśli we/wy jest w toku, hello urządzenia będą naliczane przestoju.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problemy rozwiązane w hello Update 0.2
Aktualizacja 0,2 obejmuje wszystkie zmiany z Update 0.1 w dodanie toohello poprawki opisanej w poniższej tabeli hello:

| Funkcja | Problem |
| --- | --- |
| Aktualizacje |W ostatniej wersji hello aktualizacje nie zostały wykryte automatycznie w hello klasycznego portalu Azure, tak miało toouse hello lokalnego aktualizacje tooinstall interfejsu użytkownika sieci Web. Tego problemu w tej wersji. Po zainstalowaniu aktualizacji 0,2, należy zainstalować przyszłych aktualizacji za pomocą hello klasycznego portalu Azure. |

## <a name="whats-new-in-hello-update-01"></a>What's new in hello Update 0.1
Aktualizacja 0,1 zawiera hello następujące ulepszenia i poprawki błędów. 

* **Większa odporność na awarie chmury**: Ta wersja zawiera kilka poprawek dotyczących odzyskiwania po awarii, kopii zapasowych, przywracania i Obsługa poziomów w zdarzeniu hello zakłócenia łączności chmury. 
* **Większa wydajność przywracania**: Ta wersja zawiera poprawki, które znacznie zmniejszyć czas ukończenia hello hello zadań przywracania.
* **Automatyczne odzyskiwanie optymalizacje**: usunięcie danych na woluminy alokowane elastycznie hello nieużywane magazynu bloki muszą toobe odzyskana. Tej wersji ma ulepszone hello miejsca odzyskiwanie proces z chmury hello powodujące hello nieużywane miejsce która staje się dostępna szybciej w porównaniu toohello poprzednie wersje.
* **Nowych obrazów dysku wirtualnego**: nowego wirtualnego dysku twardego, VHDX i VMDK są teraz dostępne za pośrednictwem hello klasycznego portalu Azure. Możesz pobrać te obrazy tooprovision nowych aktualizacji 0,1 urządzeń.
* **Poprawy dokładności hello stanu zadania w portalu hello**: hello starszej wersji oprogramowania, stan zadania raportowania w portalu hello nie były szczegółowego. Ten problem zostanie rozwiązany w tej wersji.
* **Środowisko sprzężenia domeny**: poprawki dotyczące dołączenie toodomain oraz zmiana nazwy urządzenia hello.

## <a name="issues-fixed-in-hello-update-01"></a>Problemy rozwiązane w hello Update 0.1
Witaj Poniższa tabela zawiera podsumowanie problemy rozwiązane w tej wersji.

| Nie. | Funkcja | Problem |
| --- | --- | --- |
| 1 |VMDK |W niektórych wersjach VMware hello dysk systemu operacyjnego został występuje jako rozrzedzony przyczyną alertów i zakłócania normalnych operacji. Problem został rozwiązany w tej wersji. |
| 2 |Serwer iSCSI |W ostatniej wersji hello hello użytkownik był wymagany toospecify bramy dla każdego interfejsu sieciowego włączone, urządzenia wirtualnego StorSimple. To zachowanie zostanie zmieniona w tej wersji, dzięki czemu hello użytkownik ma tooconfigure co najmniej jedną bramę dla wszystkich interfejsów sieciowych hello włączone. |
| 3 |Pakiet pomocy technicznej |W starszej wersji oprogramowania hello, obsługuje kolekcja pakietów nie powiodło się, gdy rozmiar pakietu hello wynosił większą niż 1 GB. Tego problemu w tej wersji. |
| 4 |Dostęp do chmury |W ostatniej wersji hello Jeśli hello tablicy wirtualnego StorSimple nie ma łączności sieciowej i został ponownie uruchomiony, hello lokalnego interfejsu użytkownika musi problemy z połączeniem. Ten problem został rozwiązany w tej wersji. |
| 5 |Monitorowanie wykresów |W poprzedniej wersji hello, następujące urządzenia trybu failover wykresy wykorzystania pojemności chmury hello wyświetlane nieprawidłowe wartości w hello klasycznego portalu Azure. Jest to stała hello bieżącej wersji. |

## <a name="known-issues-in-hello-update-01"></a>Znane problemy w hello Update 0.1
Hello Poniższa tabela zawiera podsumowanie znane problemy dla hello tablicy wirtualnego StorSimple oraz problemy hello wersji inaczej niż w poprzednich wydaniach hello. **Witaj wersji problemów wymienionych w tej wersji są oznaczone gwiazdką. Prawie wszystkie problemy hello na tej liście zostały przeniesione z wersji hello GA tablicy wirtualne StorSimple.**

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
| **14.** |Serwer plików * |Jeśli plik w folderze alternatywnych danych strumienia (AD) skojarzonych z nim, hello REKLAM nie jest kopię zapasową lub przywrócić za pomocą odzyskiwania po awarii, powielania i odzyskiwanie na poziomie elementu. | |

## <a name="next-step"></a>Następny krok
[Zainstaluj aktualizacje](storsimple-ova-install-update-01.md) na tablica wirtualne StorSimple.

