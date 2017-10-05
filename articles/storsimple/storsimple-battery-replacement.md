---
title: "Wymiana baterii urządzenia Microsoft Azure StorSimple | Dokumentacja firmy Microsoft"
description: "Opisuje sposób usunięcia, Zastąp i obsługa modułu baterii kopii zapasowych w urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a>Zastąpienie modułu baterii kopii zapasowych w urządzeniu StorSimple
## <a name="overview"></a>Omówienie
Podstawowy obudowy zasilania i chłodzenia modułu (PCM) na urządzeniu Microsoft Azure StorSimple ma dodatkowe baterii pakietu. Ten pakiet zawiera zasilania, aby urządzenia StorSimple można zapisać danych w przypadku utraty zasilaniem podstawowego systemu. Ten pakiet baterii jest określany jako *modułu kopii zapasowej baterii*. Moduł kopii zapasowej baterii istnieje tylko dla podstawowego obudowa w urządzeniu StorSimple (obudowa EBOD nie zawiera modułu baterii kopii zapasowej). 

Ten samouczek wyjaśnia, jak:

* Usuń moduł kopii zapasowej baterii 
* Zainstaluj nowy moduł kopii zapasowej baterii
* Obsługa modułu kopii zapasowej baterii

> [!IMPORTANT]
> Przed usuwanie i zastępowanie moduł kopii zapasowej baterii, zapoznaj się z informacjami bezpieczeństwa w [wprowadzenie do wymiany składników sprzętu StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-the-backup-battery-module"></a>Usuń moduł kopii zapasowej baterii
Moduł baterii kopii zapasowej dla urządzenia StorSimple jest jednostką replaceable pola. Przed zainstalowaniem w PCM modułu baterii powinny być przechowywane w oryginalnym opakowaniu. Wykonaj poniższe kroki, aby usunąć baterii kopii zapasowej.

#### <a name="to-remove-the-backup-battery-module"></a>Aby usunąć moduł kopii zapasowej baterii
1. W klasycznym portalu Azure, przejdź do **urządzeń** > **konserwacji** > **stan sprzętu**. W obszarze **współużytkowanych składników**, zobaczyć stan baterii.
2. Zidentyfikuj PCM, w którym baterii nie powiodła się. Rysunek 1 pokazuje z tyłu urządzenia StorSimple.
   
    ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-battery-replacement/IC740994.png)
   
    **Rysunek 1** obu urządzenie podstawowe przedstawiający modułów PCM i kontrolera
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Kontrolera 0 |
   | 4 |Kontrolera 1 |
   
    Jak to przedstawiono numer 3 na rysunku 2, monitorowania wskaźnika DOPROWADZIŁY na PCM 0, który odpowiada **uszkodzenia** powinny być włączone.
   
    ![Montażowa LED wskaźnik monitorowania PCM urządzenia](./media/storsimple-battery-replacement/IC740992.png)
   
    **Rysunek 2** PCM z powrotem przedstawiający monitorowania wskaźnik LED
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Ak awarii zasilania |
   | 2 |Wentylator awarii |
   | 3 |Uszkodzenia |
   | 4 |PCM OK |
   | 5 |Kontroler domeny awarii zasilania |
   | 6 |Baterii dobrej kondycji |
3. Aby usunąć PCM z baterii nie powiodło się, postępuj zgodnie z instrukcjami [Usuń PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Z PCM usunięte Podnieś Obróć uchwytu modułu baterii w górę, wskazane na poniższej ilustracji i umieszczenie jej do Usuń baterii.
   
    ![Usuwanie z PCM baterii](./media/storsimple-battery-replacement/IC741019.png)
   
    **Rysunek 3** usuwanie baterii z PCM
5. Umieść moduł jednostkę field-replaceable unit pakowania.
6. Zwraca wadliwe urządzenie do firmy Microsoft dla odpowiednich obsługi i ich obsługi.

## <a name="install-a-new-backup-battery-module"></a>Zainstaluj nowy moduł kopii zapasowej baterii
Wykonaj poniższe kroki, aby zainstalować moduł baterii zastąpienia w PCM w głównej Obudowa urządzenia StorSimple.

#### <a name="to-install-the-battery-module"></a>Aby zainstalować moduł baterii
1. Umieść odpowiednią orientację w PCM modułu baterii kopii zapasowej.
2. Przytrzymaj naciśnięty uchwytu modułu baterii, aż do miejsca łącznika.
3. Zastąpienie PCM w obudowie głównej zgodnie z wytycznymi w [Zastąp zasilania i chłodzenia modułu na urządzeniu StorSimple](storsimple-power-cooling-module-replacement.md).
4. Po zakończeniu zastąpienia, przejdź do **urządzeń** > **konserwacji** > **stan sprzętu** w klasycznym portalu Azure. Sprawdź stan baterii, aby upewnić się, że Instalacja powiodła się. Stan zielony oznacza baterii jest w dobrej kondycji.

## <a name="maintain-the-backup-battery-module"></a>Obsługa modułu kopii zapasowej baterii
W urządzeniu StorSimple modułu baterii kopii zapasowej zawiera zasilania do kontrolera podczas zdarzenia utraty zasilania. Umożliwia urządzeniu StorSimple można zapisać krytyczne dane przed zamykanie w kontrolowany sposób. Z dwóch baterii pełni obciążona w PCMs systemu może obsługiwać dwa kolejne utraty zdarzenia.

W klasycznym portalu Azure **stan sprzętu** na **konserwacji** strony wskazuje, czy działa poprawnie baterii zbliża się koniec życia. Wskazuje stan baterii **baterii w PCM 0** lub **baterii w PCM 1** w obszarze **współużytkowanych składników**. Ta strona będzie wyświetlany **OBNIŻONY** dla zbliża się z eksploatacji, i **nie powiodło się** dla osiągnięto koniec z eksploatacji. 

> [!NOTE]
> Bateria może raportować **** po prostu zajdzie potrzeba jego naliczane opłaty.
> 
> 

Jeśli **OBNIŻONY** pojawi się stan, zaleca się następujące sposobu działania:

* System może wystąpić ostatnie utraty zasilania lub baterie przeprowadzona okresowej konserwacji. Sprawdź system na 12 godzin przed kontynuowaniem.
  
  * Jeśli stan jest nadal **OBNIŻONY** po 12 godzin ciągłe połączenie AC zasilania z kontrolerami i PCMs uruchomiony, następnie baterii ma zostać zamieniony. Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) zastępczy modułu baterii kopii zapasowej.
  * Jeśli stan jest OK po 12 godzinach, bateria działa i wymagane tylko opłat konserwacji.
* Jeśli nie został skojarzony utraty zasilaniem, PCM jest włączony i podłączony do zasilania Sieciowego baterii ma zostać zamieniony. [Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) porządkowania modułu kopii zapasowej baterii zastąpienia.

> [!IMPORTANT]
> Usuwanie nie powiodło się baterii zgodnie z przepisami krajowych i regionalnych. 
> 
> 

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).

