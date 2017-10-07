---
title: "aaaDeactivate i usunąć Microsoft Azure StorSimple wirtualnego tablicą | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooremove urządzenia StorSimple z usługi najpierw dezaktywowanie go, a następnie usuwając go."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Dezaktywuj i Usuń macierz wirtualnego StorSimple

## <a name="overview"></a>Omówienie

Po dezaktywowaniu tablicą wirtualnego StorSimple, Podziel się hello połączenie między urządzeniem hello a hello odpowiedniej usługi Menedżer StorSimple urządzenia. Ten samouczek wyjaśnia, jak:

* Dezaktywować urządzenie 
* Usuwanie urządzenia dezaktywowany

informacje Hello w tym artykule dotyczą tylko tooStorSimple tablice wirtualnego. Informacji o serii 8000, zobaczyć toohow zbyt[dezaktywację lub usunięcie urządzenia](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Gdy toodeactivate?

Dezaktywacja jest operacją trwałe i nie można cofnąć. Nie można zarejestrować ponownie dezaktywować urządzenie z hello usługi Menedżer StorSimple urządzenia. Należy może toodeactivate i Usuń macierz wirtualnego StorSimple w hello następujące scenariusze:

* **Planowana praca awaryjna** : urządzenie jest w trybie online i planujesz toofail przez urządzenie. Jeśli planujesz tooupgrade tooa większych urządzenia może być konieczne toofail przez urządzenie. Po przekazania własności danych hello i hello przejścia w tryb failover, urządzenia źródłowego hello są automatycznie usuwane.
* **Nieplanowane przełączenie awaryjne** : urządzenie jest w trybie offline, należy toofail za pośrednictwem hello urządzenia. W tym scenariuszu może wystąpić podczas awarii, gdy w centrum danych hello jest awarii i urządzenia podstawowej nie działa. Planujesz toofail za pośrednictwem urządzenia pomocniczego tooa hello urządzenia. Po przekazania własności danych hello i hello przejścia w tryb failover, urządzenia źródłowego hello są automatycznie usuwane.
* **Likwidowanie** : toodecommission hello urządzenie. Wymaga to toofirst dezaktywować urządzenie hello i usuń go. Po dezaktywacji urządzenia może już uzyskać dostępu do żadnych danych, który jest przechowywany lokalnie. Można tylko dostępu i odzyskiwanie danych hello przechowywanych w chmurze hello. Jeśli planujesz danych urządzenia hello tookeep po dezaktywacji, następnie należy podjąć migawkę chmury dla wszystkich danych przed dezaktywacją urządzenia. Ta migawka w chmurze pozwala toorecover hello wszystkich danych, aby w późniejszym terminie.

## <a name="deactivate-a-device"></a>Dezaktywować urządzenie

toodeactivate urządzenie, wykonaj następujące kroki hello.

#### <a name="toodeactivate-hello-device"></a>toodeactivate hello urządzenia

1. W usłudze Przejdź zbyt**zarządzania > urządzenia**. W hello **urządzeń** bloku, kliknij i hello wybierz urządzenia, że chcesz toodeactivate.
   
    ![Wybierz urządzenie toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. W Twojej **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **... Więcej** i wybierz z listy hello **Dezaktywuj**.
   
    ![Kliknij przycisk Dezaktywuj](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. W hello **Dezaktywuj** bloku, nazwy urządzenia hello typu, a następnie kliknij przycisk **Dezaktywuj**. 
   
    ![Upewnij się, Dezaktywuj](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Witaj Dezaktywuj uruchamia proces i zajmuje kilka minut toocomplete.
   
    ![Dezaktywuj w toku](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Po dezaktywacji odświeża hello listy urządzeń.
   
    ![Dezaktywuj ukończone](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Można teraz usunąć to urządzenie.

## <a name="delete-hello-device"></a>Usuwanie urządzenia hello

Urządzenie ma pierwszy toodelete dezaktywowane toobe go. Usuwanie urządzenia spowoduje usunięcie jej z listy hello usługi toohello podłączonych urządzeń. Usługa Hello można zarządzać już hello usunąć urządzenia. dane Hello skojarzone z urządzeniem hello jednak pozostaje w chmurze hello. Te dane zostały następnie naliczone opłaty.

toodelete hello urządzenie, wykonaj następujące kroki hello.

#### <a name="toodelete-hello-device"></a>toodelete hello urządzenia

1. W Menedżerze urządzeń StorSimple, przejdź zbyt**zarządzania > urządzenia**. W hello **urządzeń** bloku, wybierz dezaktywować urządzenie, że chcesz toodelete.
2. W hello **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **... Więcej** , a następnie kliknij przycisk **usunąć**.
   
   ![Wybierz urządzenie toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. W hello **usunąć** bloku, nazwa typu hello Twoje urządzenie tooconfirm hello usunięcia, a następnie kliknij przycisk **usunąć**. Usuwanie urządzenia hello nie powoduje usunięcia danych chmury hello skojarzone z urządzeniem hello. 
   
   ![Potwierdzenie usunięcia](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. Usuwanie Hello uruchamia i zajmuje kilka minut toocomplete.
   
   ![Usuwanie w toku](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Po usunięciu urządzenia hello można wyświetlić hello aktualizacji listy urządzeń.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać informacje na temat toofail, przejdź zbyt[trybu Failover i odzyskiwania po awarii macierzy wirtualnego StorSimple](storsimple-virtual-array-failover-dr.md).

* więcej informacji o toolearn, jak hello toouse usługi Menedżer StorSimple urządzenia go za[Użyj hello tooadminister usługi Menedżer StorSimple urządzenia wirtualnego StorSimple tablica](storsimple-virtual-array-manager-service-administration.md). 

