---
title: aaaReplace kontrolera StorSimple EBOD | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak tooremove i Zastąp jeden lub oba kontrolerów EBOD na urządzeniu StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Zastąp kontrolera EBOD na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
Ten samouczek wyjaśnia sposób tooreplace uszkodzony moduł kontrolera EBOD na urządzeniu Microsoft Azure StorSimple. tooreplace moduł EBOD kontrolera, należy:

* Usuń hello błędny EBOD kontrolera
* Instalowanie nowego kontrolera EBOD

Należy wziąć pod uwagę następujące informacje, przed rozpoczęciem powitalne:

* Puste EBOD moduły muszą być wstawiane do wszystkich miejsc nieużywane. Obudowa Hello nie zostanie poprawnie cool, jeśli gnieździe pozostanie otwarte.
* Kontroler EBOD Hello jest wyłączania i można go usunąć ani zastąpić. Nie usuwaj modułu nie powiodło się, dopóki nie uzyskasz zastępczy. Po zainicjowaniu procesu wymiany hello musi zakończyć w ciągu 10 minut.

> [!IMPORTANT]
> Przed podjęciem próby wykonania tooremove lub zamienić dowolny składnik StorSimple, upewnij się, że przeglądu hello [bezpieczeństwa ikona konwencje](storsimple-safety.md#safety-icon-conventions) i innych [środki ostrożności](storsimple-safety.md).
> 
> 

## <a name="remove-an-ebod-controller"></a>Usuwanie kontrolera EBOD
Przed zastąpienie hello nie powiodło się moduł kontrolera EBOD w urządzeniu StorSimple, upewnij się, że hello inny moduł kontrolera EBOD jest aktywne i uruchomiona. Witaj następujące procedura i tabela wyjaśniono, jak tooremove Witaj EBOD moduł kontrolera.

#### <a name="tooremove-an-ebod-module"></a>Moduł EBOD tooremove
1. Otwórz hello klasycznego portalu Azure.
2. Przejdź za**urządzeń** > **konserwacji** > **stan sprzętu**i upewnij się, że stan hello hello DOPROWADZIŁA do hello active EBOD Moduł kontrolera jest zielony i hello LED modułu kontrolera EBOD hello nie powiodło się jest czerwony.
3. Znajdź moduł kontrolera EBOD hello nie powiodło się na powitania obu hello urządzenia.
4. Usuń kable hello, łączące hello EBOD kontrolera modułu toohello kontrolera przed zmianą hello EBOD modułu poza hello systemu.
5. Zanotuj hello dokładne portu SAS hello EBOD kontrolera moduł, który został połączony toohello kontrolera. Konfiguracja toothis systemu hello toorestore wymagane będzie po Zastąp hello EBOD modułu. 
   
   > [!NOTE]
   > Zazwyczaj jest to Port A, który jest oznaczony jako **hosta w** w powitania po diagramu.
   > 
   > 
   
    ![Kontroler IDE EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Rysunek 1** EBOD z powrotem modułu
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Diodę LED awarii |
   | 2 |Power LED |
   | 3 |Złączy SAS |
   | 4 |LED SAS |
   | 5 |Porty szeregowe fabryki wyłącznie do użytku |
   | 6 |Port (hosta) |
   | 7 |Port B (Host out) |
   | 8 |Port C (tylko w przypadku używania fabryki) |

## <a name="install-a-new-ebod-controller"></a>Instalowanie nowego kontrolera EBOD
Hello następujące procedura i tabela wyjaśniają sposób tooinstall moduł kontrolera EBOD w urządzeniu StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall EBOD kontrolera
1. Sprawdź urządzenie EBOD hello za szkody, szczególnie toohello interfejsu łącznika. Nie należy instalować hello nowego kontrolera EBOD, jeśli zgięte żadnych kodów PIN.
2. Otwórz pozycji, moduł hello slajdów hello obudowy do momentu Uwzględnij zamków hello zamków hello w hello.
   
    ![Instalowanie kontrolera EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Rysunek 2** instalowanie hello EBOD kontrolera modułu
3. Zamknij hello zatrzaśnięcia. Kliknięcie usłyszeć jako angażujący hello zatrzaśnięcia.
   
    ![Zwalnianie zatrzaśnięcia EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Rysunek 3** zamknięcie zatrzaśnięcia modułu EBOD hello
4. Ponownie podłącz kable hello. Użyj hello dokładnej konfiguracji, która znajdowała się przed hello zastąpienia. Zobacz powitania po diagram i tabeli, aby uzyskać szczegółowe informacje o tym, jak tooconnect hello kable.
   
    ![Podłączanie kabli do urządzenia 4U zasilania](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Rysunek 4**. Ponownie podłączyć kable
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Obudowa podstawowego |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Kontrolera 0 |
   | 5 |Kontrolera 1 |
   | 6 |EBOD kontrolera 0 |
   | 7 |EBOD kontrolera 1 |
   | 8 |Obudowa EBOD |
   | 9 |Jednostki dystrybucji zasilania |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).

