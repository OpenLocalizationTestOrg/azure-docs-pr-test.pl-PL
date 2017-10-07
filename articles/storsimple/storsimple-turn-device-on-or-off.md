---
title: "aaaTurn urządzenia serii StorSimple 8000 lub wyłącz | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak włączyć urządzenie, które zostało zamknięte lub utraty zasilania tooturn na nowym urządzeniu StorSimple i wyłączyć urządzenie uruchomione."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Włącz lub wyłącz urządzenie serii StorSimple 8000
## <a name="overview"></a>Omówienie
Wyłączanie urządzenia Microsoft Azure StorSimple nie jest wymagane w ramach normalnego działania. Jednak może być konieczne tooturn na nowe urządzenie lub urządzenia, które ma toobe zamknięta. Ogólnie rzecz biorąc wyłączania jest wymagany w przypadku których należy wymienić sprzęt nie powiodło się, fizycznie przenieść jednostkę lub podjąć urządzenia z usługi. W tym samouczku opisano procedurę hello wymagane włączanie i wyłączanie urządzenia StorSimple w różnych scenariuszach.

## <a name="turn-on-a-new-device"></a>Włącz nowe urządzenie
Witaj instrukcjami w celu włączenia na urządzeniu StorSimple na powitania po raz pierwszy różnią się w zależności od tego, czy urządzenie hello jest 8100 lub 8600 modelu. Hello 8100 ma jednej obudowie głównej hello 8600 jest urządzeniem podwójnego obudowy z głównej obudowy i obudowy EBOD. Witaj szczegółowy opis kroków, w przypadku obu modeli są objęte hello następujące sekcje.

* [Nowe urządzenie z głównej obudowa tylko](#new-device-with-primary-enclosure-only)
* [Nowe urządzenie z EBOD obudowy](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Nowe urządzenie z głównej obudowa tylko
model Hello StorSimple 8100 jest obudowa pojedynczego urządzenia. Urządzenie zawiera nadmiarowe zasilania i chłodzenia modułów (PCMs). Zarówno PCMs muszą być zainstalowane i połączone toodifferent power źródeł tooensure wysokiej dostępności.

Wykonaj następujące kroki toocable hello urządzenia zasilania.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Ukończenie konfiguracji urządzenia i okablowanie instrukcje Przejdź zbyt[zainstalować do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md). Upewnij się, wykonaj instrukcje hello dokładnie.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Nowe urządzenie z EBOD obudowy
model Hello StorSimple 8600 ma głównej obudowy oraz obudowy EBOD. Wymaga to toobe jednostki hello kablem razem łączności Serial Attached SCSI (SAS) i zasilania.

Podczas konfigurowania tego urządzenia do powitania po raz pierwszy, należy wykonać czynności hello SAS najpierw okablowania i następnie pełne hello kroki okablowania zasilania.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Ukończenie konfiguracji urządzenia i okablowanie instrukcje Przejdź zbyt[zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md). Upewnij się, wykonaj instrukcje hello dokładnie.

## <a name="turn-on-a-device-after-shutdown"></a>Włącz na urządzeniu po zamknięciu systemu
kroki Hello włączania urządzenia StorSimple, po jego zamknięciu są różne w zależności od tego, czy urządzenie hello jest 8100 lub 8600 modelu. Hello 8100 ma jednej obudowie głównej hello 8600 jest urządzeniem podwójnego obudowy z głównej obudowy i obudowy EBOD.

* [Urządzenia z głównej obudowa tylko](#device-with-primary-enclosure-only)
* [Urządzenia z EBOD obudowy](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Urządzenia z głównej obudowa tylko
Po zamknięciu Użyj hello następujące procedury tooturn na urządzeniu StorSimple z głównej obudowy i obudowy nie EBOD.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn na urządzeniu z tylko podstawowy obudowy
1. Upewnij się, że zasilania hello zmienia się na obu zasilania i chłodzenia moduły (PCMs) hello OFF pozycji. Jeśli przełączniki hello nie znajdują się w pozycji OFF hello, następnie przerzucić toohello OFF pozycji i poczekaj toogo świateł hello off.
2. Włącz urządzeń hello przestawiając przełączniki power hello na obu PCMs toohello ON pozycji. Witaj urządzenia należy włączyć.
3. Hello wyboru po tooverify, który hello urządzenie jest w pełni:
   
   1. Witaj LED OK na obu modułów PCM są zielone.
   2. Stan Hello LED na obu kontrolerów są zielony.
   3. powitalne migotania niebieski LED na jeden z kontrolerów hello co oznacza, że ten kontroler hello jest aktywna.
      
      Jeśli te warunki nie są spełnione, urządzenie nie jest dobra. Sprawdź [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Urządzenia z EBOD obudowy
Po zamknięciu Użyj hello następujące procedury tooturn na urządzeniu StorSimple z głównej obudowy i obudowy EBOD. Dokładnie zgodnie z opisem wykonywania każdego kroku w sekwencji. Błąd toodo mogłoby to spowodować utratę danych.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn na urządzeniu z podstawowym i obudowy EBOD
1. Upewnij się, że w tym hello obudowa EBOD jest połączonych toohello obudowa podstawowego. Aby uzyskać więcej informacji, zobacz [zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Upewnij się, że hello zasilania i chłodzenia modułów (PCMs) zarówno hello EBOD i obudowy głównej znajdują się w pozycji OFF hello. Jeśli przełączniki hello nie znajdują się w pozycji OFF hello, następnie przerzucić toohello OFF pozycji i poczekaj toogo świateł hello off.
3. Włącz hello obudowa EBOD najpierw przestawiając przełączniki power hello na obu PCMs toohello ON pozycji. Witaj LED PCM powinna być zielona. Zielony kontrolera EBOD LED w tej jednostce oznacza obudowa EBOD hello na.
4. Włącz obudowa głównej hello przestawiając przełączniki power hello na obu pozycji ON toohello PCMs. Witaj całego systemu powinno być teraz na.
5. Sprawdź, czy hello LED SAS są zielone, co zapewnia to połączenie hello między hello obudowa EBOD i obudowy głównej hello jest dobra.

## <a name="turn-on-a-device-after-a-power-loss"></a>Włącz na urządzeniu po utracie zasilania
Awarii zasilania lub przerwania można wyłączyć urządzenie StorSimple. Hello zasilaniu może się zdarzyć na jeden z zasilacze hello lub obu zasilacze. kroki odzyskiwania Hello są różne w zależności od tego, czy urządzenie hello jest 8100 lub 8600 modelu. Hello 8100 ma jednej obudowie głównej hello 8600 jest urządzeniem podwójnego obudowy z głównej obudowy i obudowy EBOD. W tej sekcji opisano procedury odzyskiwania powitania dla każdego scenariusza.

* [Urządzenia z głównej obudowa tylko](#8100)
* [Urządzenia z EBOD obudowy](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Urządzenia z głównej obudowa tylko<a name="8100">
Hello system kontynuować jego normalnej pracy przypadku tooone utraty zasilania z jego zasilacze. Jednak tooensure wysokiej dostępności urządzeń hello przywracania zasilania toohello zasilacz tak szybko, jak to możliwe.

Jeśli istnieje awarii zasilania lub awarii zasilania na obu zasilacze, hello system zostanie zamknięty w sposób uporządkowany i kontrolowane. Po przywróceniu zasilania hello hello system automatycznie spowoduje włączenie.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Urządzenia z EBOD obudowy<a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Podaj utraty zasilania na jednym zasilania
Hello system kontynuować jego normalnej pracy przypadku tooone utraty zasilania z jego zasilacze obudowa głównej hello lub hello EBOD obudowy. Jednak tooensure wysokiej dostępności urządzenia hello Przywróć zasilania energią toohello tak szybko, jak to możliwe.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Zarówno zasilacze na podstawowym i obudowy EBOD utraty zasilania
W przypadku awarii zasilania awarii lub zasilania na obu zasilacze hello obudowa EBOD zostanie natychmiast zamknięty i obudowy głównej hello zostanie zamknięty w sposób uporządkowany i kontrolowane. Po przywróceniu zasilania hello urządzenia zostanie uruchomiony automatycznie.

Hello power jest wyłączany ręcznie, wykonaj hello następujące kroki toorestore zasilania toohello systemu.

1. Włącz hello EBOD obudowy.
2. Po hello obudowa EBOD jest włączona, należy włączyć obudowa głównej hello.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Zarówno zasilacze w obudowie EBOD utraty zasilania
Po skonfigurowaniu kable musi zapewnić, że hello EBOD nigdy nie jest połączony tylko tooa oddzielnych PDU. Jeśli hello EBOD i obudowy głównej się nie powieść w hello tym samym czasie hello systemu zostanie wznowione.

Jeśli tylko hello EBOD obudowy nie powiedzie się na obu zasilacze, hello systemu nie będzie automatycznie odzyskać. Podjąć następujące kroki tooturn w systemie hello hello i przywróć ją tooa dobrej kondycji:

1. Jeśli obudowy głównej hello jest włączona, wyłącz zarówno zasilania i chłodzenia modułów (PCMs).
2. Poczekaj kilka minut, aż tooshut systemu hello w dół.
3. Włącz hello EBOD obudowy.
4. Po hello obudowa EBOD jest włączona, należy włączyć obudowa głównej hello.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Włącz urządzenie po hello podstawowego i EBOD obudowa połączenie zostanie przerwane
Jeśli hello powoduje utratę połączenia między kontrolerem rezerwy hello i odpowiedniego kontrolera EBOD hello, urządzenia hello nadal toowork. W przypadku utraty hello połączenie między hello systemu aktywnym kontrolerze i odpowiedniego kontrolera EBOD hello trybu failover powinny występować i hello urządzenie powinno być kontynuowane toowork normalnie.

Gdy zarówno kable Serial Attached SCSI (SAS) zostaną usunięte lub jest Przerwano połączenie hello między hello obudowa EBOD i obudowy głównej hello, urządzenia hello przestanie działać. W tym momencie wykonać hello następujące kroki.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn na urządzeniu powitania po połączenie zostanie przerwane
1. Witaj dostępu obu hello urządzenia.
2. Jeśli hello połączenie kablowe SAS między hello EBOD obudowy i obudowy głównej hello jest uszkodzona, wszystkie lane SAS LED na powitania EBOD obudowa będzie poza.
3. Zamknij zarówno zasilania i chłodzenia modułów (PCMs) na powitania EBOD obudowy i obudowy głównej hello.
4. Zaczekaj, aż wszystkie świateł hello na powitania obu zarówno obudów hello wyłączyć.
5. Włóż hello kabli SAS i upewnij się, że istnieje połączenie między hello EBOD obudowy i obudowy głównej hello.
6. Włącz hello obudowa EBOD najpierw przestawiając zarówno PCM przełączniki toohello ON pozycji.
7. Sprawdź, czy obudowa EBOD hello jest na, sprawdzając LED hello zielony ma wartość ON.
8. Włącz hello obudowa podstawowego.
9. Sprawdź, czy obudowa głównej hello jest na, sprawdzając LED kontrolera zielony hello znajduje się na.
10. Sprawdź, czy tego hello EBOD obudowa połączenia z głównej obudowa hello jest dobrym sprawdzając tego lane SAS hello LED (cztery na kontroler EBOD) znajdują się na.

> [!IMPORTANT]
> Jeśli kabli SAS hello jest uszkodzony lub hello połączenia między hello obudowa EBOD i obudowy głównej hello nie są odpowiednie, po włączeniu systemu hello, przejdzie do trybu odzyskiwania. Sprawdź [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) w takim przypadku.


## <a name="turn-off-a-running-device"></a>Wyłączanie uruchomionych urządzenia
Uruchomione urządzenia StorSimple może być konieczne toobe zamknięta, jeśli jest przenoszony, podjęte poza usługi lub został nieprawidłowo działający składnik, który musi toobe zastąpione. kroki Hello są różne w zależności od tego, czy urządzenie StorSimple hello jest 8100 lub 8600 modelu. Hello 8100 ma jednej obudowie głównej hello 8600 jest urządzeniem podwójnego obudowy z głównej obudowy i obudowy EBOD. W tej sekcji szczegółowo tooshut kroki hello dół uruchomionych urządzenia.

* [Urządzenia z głównej obudowy](#8100a)
* [Urządzenia z EBOD obudowy](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Urządzenia z głównej obudowy<a name="8100a">
tooshut dół urządzenia hello w sposób uporządkowany i kontrolowane, możesz zrobić to za pośrednictwem hello klasycznego portalu Azure lub za pośrednictwem hello środowiska Windows PowerShell dla urządzenia StorSimple. 

> [!IMPORTANT]
> Nie są zamykane uruchomionych urządzenia przy użyciu przycisku zasilania hello na powitania obu hello urządzenia.
> 
> Przed zamknięciem hello urządzenia, upewnij się, czy wszystkie składniki hello są w dobrej kondycji. W hello klasycznego portalu Azure, przejdź zbyt**urządzeń** > **konserwacji** > **stan sprzętu**i sprawdź stan wszystkich hello składniki jest zielony. Dotyczy to tylko w przypadku dobrej kondycji systemu. Jeśli hello system jest zamknięta tooreplace nieprawidłowo działający składnik, zostanie wyświetlony nie powiodło się (czerwony) lub nieprawidłowe działanie stan (żółty) dla odpowiednich składników hello w hello **stan sprzętu**.
> 
> 

Po uzyskaniu dostępu hello środowiska Windows PowerShell dla StorSimple lub hello klasycznego portalu Azure, wykonaj kroki hello w [wyłączyć urządzenie StorSimple](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Urządzenia z EBOD obudowy<a name="8600a">
> [!IMPORTANT]
> Przed zamknięciem hello obudowy podstawowego i obudowy EBOD hello, upewnij się, że wszystkie składniki hello są w dobrej kondycji. W portalu Azure hello kolejno zbyt**urządzeń** > **Monitor** > **kondycji sprzętu**i sprawdź, czy wszystkie składniki hello są w dobrej kondycji.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut dół uruchomionych urządzenia z EBOD obudowy
1. Wykonaj wszystkie kroki hello na liście [zamknięcia urządzenia StorSimple](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) dla hello obudowa podstawowego.
2. Po hello obudowa podstawowy jest zamknięta, zamknij hello EBOD przestawiając poza przełączników zarówno zasilania i chłodzenia modułu (PCM).
3. tooverify, który hello EBOD została zamknięta, sprawdź, czy wszystkie świateł na powitania obu obudowa EBOD hello są wyłączone.

> [!NOTE]
> nie należy usuwać Hello kabli SAS, które są używane tooconnect hello EBOD obudowa toohello głównej obudowa dopiero po zamknięciu systemu hello.

## <a name="next-steps"></a>Następne kroki
[Skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) w razie wystąpienia problemów podczas Włączanie lub wyłączanie urządzenia StorSimple.

