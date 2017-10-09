---
title: "aaaReplace baterii na urządzeniu serii Microsoft Azure StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooremove, Zastąp i obsługa modułu kopii zapasowej baterii hello na urządzeniu StorSimple."
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
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>Zastąp hello modułu baterii kopii zapasowych w urządzeniu StorSimple

## <a name="overview"></a>Omówienie
obudowy głównej Hello zasilania i chłodzenia modułu (PCM) na urządzeniu Microsoft Azure StorSimple ma dodatkowe baterii pakietu. Ten pakiet zawiera zasilania, dzięki czemu hello urządzenia StorSimple można zapisać danych w przypadku utraty AC zasilania toohello głównej obudowy. Ten pakiet baterii jest hello określonego tooas *modułu kopii zapasowej baterii*. Moduł kopii zapasowej baterii Hello istnieje tylko dla podstawowego obudowa hello w urządzeniu StorSimple (hello obudowa EBOD nie zawiera modułu baterii kopii zapasowej).

Ten samouczek wyjaśnia, jak:

* Usuń moduł kopii zapasowej baterii hello
* Zainstaluj nowy moduł kopii zapasowej baterii
* Obsługa modułu kopii zapasowej baterii hello

> [!IMPORTANT]
> Przed usuwanie i zastępowanie moduł kopii zapasowej baterii, przejrzyj informacje bezpieczeństwa hello w hello [wymiana składników sprzętowych tooStorSimple wprowadzenie](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-hello-backup-battery-module"></a>Usuń moduł kopii zapasowej baterii hello
Hello modułu baterii kopii zapasowej dla urządzenia StorSimple jest jednostką replaceable pola. Przed zainstalowaniem w hello PCM modułu baterii hello powinny być przechowywane w oryginalnym opakowaniu. Wykonaj następujące kroki tooremove hello kopii zapasowej baterii hello.

#### <a name="tooremove-hello-backup-battery-module"></a>Moduł kopii zapasowej baterii hello tooremove
1. W hello portalu Azure Przejdź bloku usługi Menedżer StorSimple urządzenia tooyour. Przejdź za**urządzeń** , a następnie wybierz urządzenie z listy urządzeń hello. Przejdź za**Monitor** > **kondycji sprzętu**. W obszarze **współużytkowanych składników**, przyjrzeć się stan hello hello baterii.
2. Zidentyfikuj PCM hello, w których hello baterii nie powiodła się. Rysunek 1 pokazuje hello obu hello urządzenia StorSimple.
   
    ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-battery-replacement/IC740994.png)
   
    **Rysunek 1** obu urządzenie podstawowe przedstawiający modułów PCM i kontrolera
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Kontrolera 0 |
   | 4 |Kontrolera 1 |
   
    Jak pokazano numerem 3 hello na rysunku 2, hello monitorowania wskaźnik DOPROWADZIŁY na PCM 0, który odpowiada za**uszkodzenia** powinny być włączone.
   
    ![Montażowa LED wskaźnik monitorowania PCM urządzenia](./media/storsimple-battery-replacement/IC740992.png)
   
    **Rysunek 2** hello przedstawiający PCM z powrotem monitorowania wskaźników
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Ak awarii zasilania |
   | 2 |Wentylator awarii |
   | 3 |Uszkodzenia |
   | 4 |PCM OK |
   | 5 |Kontroler domeny awarii zasilania |
   | 6 |Baterii dobrej kondycji |
3. Witaj tooremove PCM z baterii nie powiodło się, wykonaj kroki hello w [Usuń PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Hello PCM usunięte, przyrostu i baterii hello Obróć moduł obsługi górę wskazane powitania po rysunek, a obudowach go tooremove hello baterii.
   
    ![Usuwanie z PCM baterii](./media/storsimple-battery-replacement/IC741019.png)
   
    **Rysunek 3** usuwanie baterii hello z hello PCM
5. Moduł hello miejsce w jednostce replaceable pola hello pakowania.
6. Zwróć hello tooMicrosoft urządzenie do właściwego obsługi i obsługi.

## <a name="install-a-new-backup-battery-module"></a>Zainstaluj nowy moduł kopii zapasowej baterii
Wykonaj następujące kroki tooinstall hello zastępczy baterii modułu w hello PCM w obudowie głównej hello urządzenia StorSimple hello.

#### <a name="tooinstall-hello-battery-module"></a>Moduł baterii hello tooinstall
1. Umieść moduł kopii zapasowej baterii hello hello odpowiednią orientację w hello PCM.
2. Naciśnij klawisz hello baterii modułu obsługi wszystkich hello sposób tooseat hello łącznika.
3. Zastąp hello PCM w obudowie głównej hello przez następujące wytyczne hello w [Zastąp zasilania i chłodzenia modułu na urządzeniu StorSimple](storsimple-power-cooling-module-replacement.md).
4. Po zakończeniu hello zastąpienie go tooyour urządzenia, a następnie przejdź zbyt**Monitor** > **kondycji sprzętu** w hello portalu Azure. Sprawdź stan hello hello baterii toomake się upewnić, że hello instalacja zakończyła się pomyślnie. Stan zielony oznacza baterii hello jest w dobrej kondycji.

## <a name="maintain-hello-backup-battery-module"></a>Obsługa modułu kopii zapasowej baterii hello
W urządzeniu StorSimple hello kopii zapasowej baterii modułu zawiera kontroler toohello energią podczas zdarzenia utraty zasilania. Umożliwia hello StorSimple urządzenia toosave krytyczne dane przed tooshutting w dół w kontrolowany sposób. Z dwóch baterii pełni obciążona w hello PCMs hello systemu może obsługiwać dwa kolejne utraty zdarzenia.

W portalu Azure hello, hello **kondycji sprzętu** w obszarze hello **Monitor** bloku wskazuje, czy działa poprawnie baterii hello zbliża się hello z wycofanych. Wskazuje stan baterii Hello **baterii w PCM 0** lub **baterii w PCM 1** w obszarze **współużytkowanych składników**. Wyświetli ten blok **OBNIŻONY** dla zbliża się z eksploatacji, i **** dla osiągnięto koniec z eksploatacji.

> [!NOTE]
> zgłosić baterii Hello **** gdy po prostu potrzebuje toobe obciążona.


Jeśli hello **OBNIŻONY** pojawi się stan, firma Microsoft zaleca powitania od sposobu działania:

* Hello system mogła wystąpić ostatnie utraty zasilania lub baterie hello przeprowadzona okresowej konserwacji. Sprawdź hello system na 12 godzin przed kontynuowaniem.
  
  * Jeśli stan hello jest nadal **OBNIŻONY** po 12 godzin zasilania tooAC stałego połączenia z hello kontrolerów i PCMs uruchomiony, następnie hello poziomie naładowania baterii musi toobe zastąpione. Sprawdź [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) zastępczy modułu baterii kopii zapasowej.
  * Jeśli stan hello staje się OK po 12 godzinach, baterii hello działa i wymagane tylko opłat konserwacji.
* Jeśli nie nastąpiła skojarzone utraty zasilania Sieciowego i hello PCM jest włączony i podłączony tooAC zasilania, hello poziomie naładowania baterii musi toobe zastąpione. [Skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder modułu kopii zapasowej baterii zastąpienia.

> [!IMPORTANT]
> Usuń hello nie baterii zgodnie z toonational i przepisy regionalne.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).

