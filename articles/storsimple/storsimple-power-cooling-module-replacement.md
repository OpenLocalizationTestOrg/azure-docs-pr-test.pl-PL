---
title: "aaaReplace PCM na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooremove i Zamień hello zasilania i chłodzenia modułu (PCM) na urządzeniu StorSimple"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Zamień na urządzeniu StorSimple zasilania i chłodzenia modułu
## <a name="overview"></a>Omówienie
Hello zasilania i chłodzenia modułu (PCM) w urządzeniu Microsoft Azure StorSimple składa się z źródła zasilania i chłodzenia wentylatory, które są kontrolowane przez hello podstawowego i obudowy EBOD. Istnieje tylko jeden model PCM, który jest certyfikowany do każdej obudowy. Obudowa głównej Hello jest certyfikowany do 764 W PCM i obudowy EBOD hello jest certyfikowany do 580 W PCM. Mimo że hello PCMs obudowa głównej hello i obudowy EBOD hello są różne, hello zastępczy procedura jest identyczna.

Ten samouczek wyjaśnia, jak:

* Usuń PCM
* Zainstaluj serwer zamienny PCM

> [!IMPORTANT]
> Przed usunięcie i zastąpienie PCM, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="before-you-replace-a-pcm"></a>Aby zastąpić PCM
Należy zwrócić uwagę na następujące istotne problemy przed wymianą programu PCM hello:

* Zasilacz hello z hello PCM nie powiedzie się, pozostaw hello zainstalowany moduł uszkodzony, ale Usuń hello przewód zasilający. Wentylator Hello będzie kontynuowana tooreceive zasilania z obudowy hello i kontynuować tooprovide właściwego chłodzenia. W przypadku niepowodzenia wentylator hello hello PCM musi toobe natychmiast zastąpione.
* Przed usunięciem hello PCM, rozłączyć zasilania hello hello PCM wyłączając hello przełącznika głównego (o ile istnieje) lub usuwając fizycznie hello przewód zasilający. Zapewnia to system tooyour ostrzeżenie, że wyłączania zasilania jest bezpośrednie.
* Upewnij się, że inne PCM będzie działać dla tego powitalne nadal działania systemu przed zastępowanie hello PCM uszkodzony. Błędny PCM muszą zostać zastąpione pełnej funkcjonalności PCM tak szybko, jak to możliwe.
* Zastąpienie modułu PCM zajmuje tylko kilka minut toocomplete, ale musi zostać ukończone w ciągu 10 minut usunięcia przegrzaniu tooprevent PCM hello nie powiodło się.
* Należy pamiętać, hello zastępczy 764 W PCM modułów wysłane z fabryki hello nie zawierają hello modułu baterii kopii zapasowej. Zostanie potrzebuje baterii hello tooremove z programu PCM uszkodzony i wstawić go w hello zastąpienie modułu wcześniejsze tooperforming hello zastąpienia. Aby uzyskać więcej informacji, zobacz temat jak zbyt[usuwanie i wstawianie modułu baterii kopii zapasowej](storsimple-battery-replacement.md).

## <a name="remove-a-pcm"></a>Usuń PCM
Wykonaj te instrukcje, gdy są gotowe tooremove zasilania i chłodzenia modułu (PCM) z urządzenia Microsoft Azure StorSimple.

> [!NOTE]
> Przed usunięciem programu PCM, sprawdź, czy poprawne zastąpienia (764 T dla hello obudowa podstawowego) lub 580 W dla hello EBOD obudowy.
> 
> 

#### <a name="tooremove-a-pcm"></a>tooremove PCM
1. W hello klasycznego portalu Azure, kliknij przycisk **urządzeń** > **konserwacji** > **stan sprzętu**. Sprawdź stan hello hello PCM składników w obszarze **współużytkowanych składników** tooidentify, który PCM nie powiodła się:
   
   * Jeśli zasilacz w PCM 0 nie powiodła się, stan hello **zasilacz w PCM 0** czerwony.
   * Jeśli zasilacz 1 PCM nie powiodła się, stan hello **zasilacz 1 PCM** czerwony.
   * Jeśli wentylator hello PCM 1 nie powiodło się, stan hello **chłodzenia 0 dla PCM 0** lub **chłodzenia 1 dla PCM 0** czerwony.
2. Zlokalizuj hello PCM nie powiodło się na powitania kopii hello głównej załącznika. Jeśli używasz modelu 8600 zidentyfikować obudowa głównej hello analizując hello numeru identyfikacyjnego jednostki systemu wyświetlane na ekranie panelu przedniego LED hello. Witaj domyślny jest wyświetlany na hello obudowa podstawowy identyfikator jednostki **00**, a domyślny hello identyfikator jednostki jest wyświetlany na powitania obudowa EBOD **01**. Hello następujący diagram i tabeli opisano hello panelu przedniego hello LED wyświetlania.
   
    ![Identyfikator systemu na panelu przednim OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Rysunek 1** panelu przodu hello urządzenia  
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Przycisk wyciszenia |
   | 2 |Zasilania systemu |
   | 3 |Błąd modułu |
   | 4 |Błąd logiczny |
   | 5 |Wyświetlanie Identyfikatora jednostki |
3. można także Hello monitorowania LED wskaźnika w hello obu obudowa głównej hello tooidentify hello PCM uszkodzony. Zobacz następujące hello diagram i jak tabela toounderstand toouse hello LED toolocate hello PCM uszkodzony. Na przykład, jeśli hello DOPROWADZIŁY odpowiedniego toohello **wentylator się nie powieść** jest włączone, wentylator hello nie powiodło się. Podobnie, jeśli hello DOPROWADZIŁY odpowiadającego zbyt**AC niepowodzenie** jest włączone, hello zasilania nie powiodło się. 
   
    ![Płyty montażowej wskaźnika monitorowania urządzenia PCM LED](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Rysunek 2** PCM z powrotem z wskaźnik LED
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Ak awarii zasilania |
   | 2 |Wentylator awarii |
   | 3 |Uszkodzenia |
   | 4 |PCM OK |
   | 5 |Kontroler domeny awarii zasilania |
   | 6 |Baterii dobrej kondycji |
4. Zobacz toohello po diagram hello obu hello StorSimple urządzenia toolocate hello nie powiodło się PCM modułu. PCM 0 jest po lewej stronie powitania i PCM 1 znajduje się na powitania prawo. Witaj poniższej tabeli opisano hello modułów.
   
     ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Rysunek 3** obu urządzenia z wtyczki 
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Kontrolera 0 |
   | 4 |Kontrolera 1 |
5. Włącz wylogowywać hello PCM uszkodzony i Odłącz hello zasilający dostaw. Można teraz usunąć hello PCM.
6. Ujmij zatrzaśnięcia hello i stronie powitania hello PCM obsługi między thumb i wskazującym i zmieścić je razem tooopen hello dojścia.
   
    ![Otwierania PCM dojścia](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Rysunek 4** hello otwierania PCM obsługi
7. Witaj uchwytu obsługi i Usuń hello PCM.
   
    ![Usuwanie urządzenia PCM](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Rysunek 5** hello usunięcie PCM

## <a name="install-a-replacement-pcm"></a>Zainstaluj serwer zamienny PCM
Wykonaj te instrukcje tooinstall PCM w urządzeniu StorSimple. Upewnij się, że włożono hello kopii zapasowej baterii modułu wcześniejsze tooinstalling hello zastępczy PCM (dotyczy too764 tylko W PCMs). Aby uzyskać więcej informacji, zobacz temat jak zbyt[usuwanie i wstawianie modułu baterii kopii zapasowej](storsimple-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>tooinstall PCM
1. Sprawdź, czy hello poprawne zastępuje PCM ten załącznik. Obudowa głównej Hello musi 764 W PCM i hello EBOD Obudowa musi 580 W PCM. Nie powinny podejmować toouse hello 580 PCM W w obudowie głównej hello lub hello 764 PCM W w hello EBOD obudowy. powitania po obraz pokazuje, gdzie tooidentify te informacje na powitania etykietę czyli umieszczone toohello PCM.
   
    ![Etykieta PCM urządzenia](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Rysunek 6** PCM etykiety
2. Sprawdź, czy obudowa toohello szkody, ze szczególnym uwzględnieniem toohello łączników. 
   
   > [!NOTE]
   > **Nie należy instalować hello modułu, jeśli zgięte żadnych kodów PIN łącznika.**
   > 
   > 
3. Otwórz pozycji slajdów hello modułu w obudowie hello hello PCM obsługi w hello.
   
    ![Instalowanie urządzenia PCM](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Rysunek 7** hello instalowanie PCM
4. Zamknij ręcznie hello PCM dojścia. Kliknięcie usłyszeć jako angażujący hello dojścia zatrzaśnięcia. 
   
   > [!NOTE]
   > tooensure, który hello zaangażowane mają numery PIN, należy ostrożnie holownik na uchwycie hello bez zwolnienia zatrzaśnięcia hello łącznika. Jeśli hello PCM slajdów wychodzących, oznacza to, że tego zatrzaśnięcia hello został zamknięty przed zaangażowane hello łączników.
   > 
   > 
5. Połącz źródła zasilania toohello przewodów zasilania hello i toohello PCM.
6. Zabezpiecz naprężenia hello bele zwolnienia. 
7. Włącz hello PCM.
8. Sprawdź, czy zastąpienia hello się pomyślnie: w hello klasycznego portalu Azure usługi Menedżer StorSimple, przejdź zbyt**urządzeń** > **konserwacji**  >  **Stan sprzętu**. W obszarze **współużytkowanych składników**, stan hello hello PCM powinna być zielona. 
   
   > [!NOTE]
   > Może upłynąć kilka minut, aż hello zastępczy PCM toocompletely initialize.
   > 
   > 

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).

