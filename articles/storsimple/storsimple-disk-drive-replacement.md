---
title: "aaaReplace dysku na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tooreplace dysku wpływają na obudowę głównej StorSimple lub obudowa EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a>Zamień na dysku w urządzeniu StorSimple
## <a name="overview"></a>Omówienie
Ten samouczek wyjaśnia, jak zostanie usunięty i zastąpiony nieprawidłowe działanie lub uszkodzonego dysku twardego na urządzeniu Microsoft Azure StorSimple. tooreplace dysku, musisz:

* Odłączyć hello antitamper blokady
* Usuń dysk hello
* Zainstaluj hello wymiany dysku

> [!IMPORTANT]
> Przed usunięcie i zastąpienie dysku, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="disengage-hello-antitamper-lock"></a>Odłączyć hello antitamper blokady
Ta procedura wyjaśnia sposób hello antitamper blokad na urządzeniu StorSimple można zaangażowane lub odłączony podczas zastępowania hello dysków. blokady antitamper Hello są zainstalowane w uchwytach operatora dysku hello i są one dostępne za pośrednictwem małych otwarcie w sekcji zatrzaśnięcia hello hello dojścia. Dyski są dostarczane z hello blokad zestaw toohello zablokowany pozycji.

#### <a name="toounlock-hello-antitamper-lock"></a>toounlock hello antitamper blokady
1. Starannie wstawić hello blokady klucza ("tamperproof" T10 śrubokręt, otrzymany od firmy Microsoft) do otwarcie hello w uchwyt hello i jego gniazda. 
   
   > [!NOTE]
   > Jeśli blokady antitamper hello jest aktywna, hello red wskaźnika jest widoczne w otwarcie hello.
   > 
   > 
   
    ![Zablokowane dysku](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Rysunek 1** blokady przed wykrycie zaangażowane
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |Otwarcie wskaźnika |
   | 2 |Antitamper blokady |
2. Obróć hello klucz, w przeciwnym kierunku, dopóki hello czerwony wskaźnik nie jest widoczna w otwarcie hello powyżej hello klucza.
3. Usuń klucz hello.
   
    ![Odblokowany dysku](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Rysunek 2** odblokowany dysku
4. można teraz usunąć Hello dysku.

Wykonaj kroki hello w odwrotnej tooengage hello blokady.

## <a name="remove-hello-disk-drive"></a>Usuń dysk hello
Urządzenia StorSimple obsługuje konfiguracji RAID 10 przypominającej magazynu spacji. Oznacza to, że aplikacja może działać normalnie z jednego dysku nie powiodło się, dysków półprzewodnikowych (SSD), lub dysku twardego dysku (HDD). 

> [!IMPORTANT]
> * Jeśli w systemie jest więcej niż jednego dysku nie powiodło się, nie należy usuwać więcej niż jeden dysków SSD i HDD z systemu hello w dowolnym momencie w czasie. W ten sposób może spowodować utratę danych.
> * Upewnij się, umieść zastępczy dysków SSD w miejscu, które wcześniej zawierało dysków SSD. Podobnie umieść zastępczy dysk twardy w miejscu, które wcześniej zawierało dysk twardy.
> * W hello klasycznego portalu Azure, miejsc są ponumerowane od 0 – 11. W związku z tym jeśli hello portal pokazuje, że dysk w gnieździe 2 nie powiodło się na urządzeniu hello szukać hello uszkodzony dysk w gnieździe trzeci powitania od góry powitania po lewej.
> 
> 

Dyski można usunięty i zastąpiony podczas hello systemu.

#### <a name="tooremove-a-drive"></a>tooremove dysku
1. tooidentify hello uszkodzonym dysku, w hello klasycznego portalu Azure, przejdź zbyt**urządzeń** > **konserwacji** > **stan sprzętu**. Ponieważ dysk może zakończyć się niepowodzeniem w obudowie głównej hello i/lub w obudowie EBOD (Jeśli używasz modelu 8600), przyjrzeć się stan hello hello dyski w obszarze **współużytkowanych składników** i w obszarze **EBOD obudowa współużytkowanych składników**. Uszkodzony dysk w każdej obudowie będą wyświetlane z czerwonym oznaczeniem stanu.
2. Zlokalizuj hello dysków z przodu hello obudowa głównej hello lub hello EBOD obudowy. 
3. Jeśli dysk hello jest odblokowany, przejdź toohello następnego kroku. Jeśli dysk hello jest zablokowany, odblokuj go, wykonując procedurę hello w [odłączyć blokady antitamper hello](#disengage-the-antitamper-lock).
4. Naciśnij klawisz hello czarnym zatrzaśnięć hello dysku operator modułu i ściąganie hello dysku operator uchwytu wylogowanie i optymalizacji z przodu hello hello obudowy. 
   
    ![Zwolnienie uchwytu dysku](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Rysunek 3** zwolnienie hello dysku dojścia
5. Podczas pełni rozszerzania hello dysku operator uchwytu, przesuń operatora dysku hello poza hello obudowy. 
   
    ![Przedłużanie dysku z dysku](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Rysunek 4** przedłużanie hello dysku poza hello operatora

## <a name="install-hello-replacement-disk-drive"></a>Zainstaluj hello wymiany dysku
Po dysku nie powiodło się w urządzeniu StorSimple i usunięto go, wykonaj tooreplace tej procedury za pomocą nowego dysku.

#### <a name="tooinsert-a-drive"></a>tooinsert dysku
1. Upewnij się, że dojście operatora dysku hello pełni zostanie rozszerzony, jak pokazano w powitania po obrazu.
   
    ![Dysk z dojściem rozszerzone](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Rysunek 5** dysku z dojściem rozszerzone
2. Slajd hello dysk nośnika końca hello w obudowie hello. 
   
    ![Przedłużanie dysku na dysk nośnika](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Rysunek 6** ruchomej hello dysku operatora w obudowie hello
3. Z hello dysku operatora hello wstawiony, zamknij dysk nośnika dojściem podczas kontynuowanie toopush hello dysk nośnika do hello obudowy, dopóki hello dysku operator uchwytu przyciąganie w stanie zablokowanym.
4. Użyj hello blokady klucz dostarczony przez dojście operatora hello toosecure firmy Microsoft (tamperproof Torx śrubokręt) w miejscu przez włączenie gwintowanym blokady hello Włącz kwartału z ruchem wskazówek zegara.
5. Sprawdź, czy zastąpienia hello zakończyło się pomyślnie i działa hello dysku przez uzyskanie dostępu do hello klasycznego portalu Azure i nawigacja zbyt**konserwacji** > **stan sprzętu**. W obszarze **współużytkowanych składników** lub **składniki udostępnione obudowy EBOD**, stan dysku hello powinna być zielona, wskazujący, że jest w dobrej kondycji.
   
   > [!NOTE]
   > Może upłynąć kilka godzin tooturn stan dysku hello zielonego po wymianie hello.
   > 
   > 

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).

