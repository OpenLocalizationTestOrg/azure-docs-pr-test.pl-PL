---
title: "wymiana składników sprzętowych aaaStorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toosafely zastąpienie hello PCMs, baterii, moduły kontrolera, EBOD kontrolerów, dysków i obudowy urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e8087ba7-0b66-4f59-8988-e53aad52ee21
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 472d9dc1c31b61550fe079cc9b9419510487db3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Zamień na urządzeniu z serii StorSimple 8000 składnik sprzętowy

## <a name="overview"></a>Omówienie
Zastąpienie składnika samouczki Hello opisano hello składników sprzętowych programu Microsoft Azure StorSimple 8000 serii urządzenia i hello kroki niezbędne tooremove i zastąp je. W tym artykule opisano hello bezpieczeństwa ikony, zawiera wskaźniki toohello szczegółowe samouczki i list hello składników, które są wymienne.

> [!IMPORTANT]
> Przed podjęciem próby wykonania tooremove lub zamienić dowolny składnik StorSimple, upewnij się, że przeglądu hello [bezpieczeństwa ikona konwencje](#safety-icon-conventions) i innych [środki ostrożności](storsimple-safety.md).
> 
> 

### <a name="safety-icon-conventions"></a>Konwencje ikona bezpieczeństwa
Witaj poniższej tabeli opisano hello ikon bezpieczeństwa, używanych w tych samouczkach. Zwrócić szczególną uwagę toothese bezpieczeństwa ikony, jak przechodzić przez tooremove kroki hello i Zastąp składniki.

| Ikona | Tekst | Dodatkowe informacje |
|:--- |:--- |:--- |
| ![Ikona ostrzeżenia](./media/storsimple-hardware-component-replacement/Warning.png) |**ZAGROŻENIA!** |Wskazuje niebezpiecznych sytuacji, który nie uniknąć spowoduje śmierci lub poważnej szkody. Ten wyraz sygnału jest najbardziej skrajne sytuacjach ograniczone toohello. |
| ![Ikona ostrzeżenia](./media/storsimple-hardware-component-replacement/Warning.png) |**OSTRZEŻENIE!** |Wskazuje niebezpiecznych sytuację, w której, jeśli nie jest to uniknąć, może spowodować śmierci lub poważnej szkody. |
| ![Ikonę ostrzeżenia](./media/storsimple-hardware-component-replacement/Caution.png) |**UWAGA!** |Wskazuje sytuację zagrożenia co, jeśli nie jest to uniknąć, może spowodować szkody drobne lub średniego. |
| ![Ikona powiadomienia](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**UWAGA:** |Wskazuje informacje uznawane za ważne, ale nie zagrożenia związane z. |
| ![Ikona elektrycznego uderzenia](./media/storsimple-hardware-component-replacement/Electric.png) |**Uderzenia elektrycznego zagrożenia** |Wskazuje wysokie napięcie. |
| ![Ikona ciężki](./media/storsimple-hardware-component-replacement/Weight.png) |**Ciężki** | |
| ![Brak ikony obsługiwanych części użytkownika](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Nie części obsługiwanych użytkownika** |Brak dostępu do chyba, że poprawnie uczony. |
| ![Ikona instrukcje odczytu](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Najpierw przeczytać wszystkie instrukcje** | |
| ![Ikona zagrożenie wskazówki](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Porada zagrożenia** | |

### <a name="before-you-begin"></a>Przed rozpoczęciem
Zapoznaj się z hello bezpieczeństwa informacji na temat ikony bezpieczeństwa i urządzenia używane w tym samouczku. Przejdź za[bezpiecznie zainstalowania i obsługi urządzenia StorSimple](storsimple-safety.md) pełne informacje. Należy się hello tooreview [środki ostrożności](storsimple-safety.md#handling-precautions) przed obsługi urządzenia StorSimple. 

Przed podjęciem próby tooreplace składnika, należy wziąć pod uwagę hello następujących informacji.

![Ikona ostrzeżenia](./media/storsimple-hardware-component-replacement/Warning.png) ![ikona uderzenia elektrycznego](./media/storsimple-hardware-component-replacement/Electric.png) **ostrzeżenie!** 

* Tła samodzielnie prawidłowo przy użyciu elektrostatyczne lub antistatic mat podczas obsługi modułów i składniki urządzenia StorSimple.
* Nie touch żadnych obwodu. Podczas obsługi składników, które mogą być narażone obwody hello Użyj podane dojść i przewodników.

![Ikona ostrzeżenia](./media/storsimple-hardware-component-replacement/Warning.png) ![ikony](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **POWIADOMIEŃ:**

Podczas zastępowania modułu, **nigdy nie należy pozostawiać pustego bay hello tyłu obudowy hello**. Uzyskaj zastąpienia lub pusty moduł przed usunięciem hello problem części.

## <a name="hardware-component-replacement-procedures"></a>Procedury wymiany składników sprzętu
Urządzenie serii StorSimple 8000 składa się z kilku wtyczki w hello podstawowej i/lub EBOD obudowy. Hello 8100 ma jednej obudowie głównej hello 8600 jest urządzeniem podwójną obudowa z głównej obudowy i obudowy EBOD.

hello następujące tabele przedstawiono składniki sprzętowe głównego Hello w urządzeniu. Kliknij łącze hello w hello **procedury wymiany** toohello toogo kolumny skojarzone samouczka.

| Składniki | # Obecnie | Moduł wtyczki? | Procedury wymiany |
|:--- |:--- |:--- |:--- |
| Podstawa montażowa |1 |Nie |[Zastąp podstawę hello na urządzeniu StorSimple](storsimple-chassis-replacement.md) |
| Podstawowy kontrolerów |2 |Tak |[Zastąp modułu kontroler na urządzeniu StorSimple](storsimple-controller-replacement.md) |
| 764W zasilania i chłodzenia modułów (PCMs) |2 |Tak |[Zamień na urządzeniu StorSimple zasilania i chłodzenia modułu](storsimple-power-cooling-module-replacement.md) |
| Kopia zapasowa baterii |2 |Tak |[Zastąp hello modułu baterii kopii zapasowych w urządzeniu StorSimple](storsimple-battery-replacement.md) |
| Stacje dysków |12 |Tak |[Zamień na dysku w urządzeniu StorSimple](storsimple-disk-drive-replacement.md) |

**Tabela 1** składniki sprzętowe w obudowie głównej hello

obudowy głównej Hello i obudowy EBOD hello różnią się w ich modułów we/wy. Ponadto hello PCMs mają różne moc. PCMs Hello w obudowie głównej hello 764 W, są w hello obudowa EBOD 580 W. PCMs hello w głównej hello obudowa również zawierać modułu baterii kopii zapasowej.

| Składniki | # Obecnie | Moduł wtyczki? | Procedury wymiany |
|:--- |:--- |:--- |:--- |
| Podstawa montażowa |1 |Nie |[Zastąp podstawę hello na urządzeniu StorSimple](storsimple-chassis-replacement.md) |
| Kontrolery EBOD |2 |Tak |[Zastąp kontrolera EBOD na urządzeniu StorSimple](storsimple-ebod-controller-replacement.md) |
| 580W zasilania i chłodzenia modułów (PCMs) |2 |Tak |[Zamień na urządzeniu StorSimple zasilania i chłodzenia modułu](storsimple-power-cooling-module-replacement.md) |
| Stacje dysków |12 |Tak |[Zamień na dysku w urządzeniu StorSimple](storsimple-disk-drive-replacement.md) |

**Tabela 2** składniki sprzętowe w hello obudowa EBOD

wtyczki Hello na urządzeniu hello są wyróżnione na powitania po diagramy front i tylne. Można użyć lokalizacji hello toodetermine diagramy te hello na różnych wtyczki Jeśli zastępczy jest wymagana. Hello front diagram pokazuje hello dysków oraz hello tylnej diagramów hello EBOD obudowy i obudowy głównej hello Pokaż hello wtyczki.

![Frontplane urządzenia z dyskami](./media/storsimple-hardware-component-replacement/IC741028.png)

**Rysunek 1** Front hello urządzenia

| Etykieta | Opis |
|:--- |:--- |
| 0 - 11 |Stacje dysków (łącznie z 12) |

Zarówno hello obudowa podstawowego, jak i obudowy EBOD hello ma dysk nośnika modułów. Podstawa montażowa Hello przechowuje dwanaście 3,5" dyski w formacie 3 na 4.

![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-hardware-component-replacement/IC740994.png)

**Rysunek 2** obu hello obudowa podstawowego

| Etykieta | Opis |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Kontrolera 0 |
| 4 |Kontrolera 1 |

![Montażowa urządzenia EBOD obudowa wtyczki](./media/storsimple-hardware-component-replacement/IC769599.png)

**Rysunek 3** obu hello obudowa EBOD

| Etykieta | Opis |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |EBOD kontrolera 0 |
| 4 |EBOD kontrolera 1 |

## <a name="field-replaceable-units"></a>Pole jednostki
Witaj następujące pola jednostki FRU (FRU) są dostępne dla urządzenia StorSimple:

* Podstawa montażowa (w tym panelu Operacje zintegrowane hello)
* 764 W AC PCM
* 580 W AC PCM
* Dysk twardy z modułem operatora dysku
* Moduł kontrolera
* Moduł kontrolera EBOD
* Moduł kopii zapasowej baterii
* Instalowanie zestawu kolei stojak

Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) tooorder żadnego z tych jednostek zastąpienia.

## <a name="next-steps"></a>Następne kroki
Przejrzyj wszystkie [bezpieczeństwa informacji](storsimple-safety.md) przed podjęciem próby tooreplace składnik sprzętowy StorSimple.

