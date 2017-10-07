---
title: "aaaDeactivate i usuwanie urządzenia z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooremove urządzenia StorSimple z usługi najpierw dezaktywowanie go, a następnie usuwając go."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Dezaktywuj i usuwanie urządzenia StorSimple

## <a name="overview"></a>Omówienie

W tym artykule opisano sposób toodeactivate i usuwanie urządzenia StorSimple, który jest połączony tooa usługi Menedżer StorSimple urządzenia. wskazówki Hello w tym artykule dotyczą tylko tooStorSimple 8000 urządzeń z serii tym hello StorSimple chmury urządzenia. Jeśli korzystasz z tablicą wirtualnego StorSimple, następnie przejdź zbyt[Dezaktywuj i delete dla tablicy wirtualnego StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Dezaktywacja serwery hello połączenie między urządzeniem hello a hello odpowiedniej usługi Menedżer StorSimple urządzenia. Możesz tootake urządzenia StorSimple poza usługi (na przykład, jeśli są zastępowanie lub uaktualnianie urządzenia lub jeśli już używasz StorSimple). Jeśli tak, potrzebujesz toodeactivate hello urządzenia, aby można było go usunąć.

Po dezaktywacji urządzenia żadnych danych, które były przechowywane lokalnie na urządzeniu hello nie jest już dostępny. Można odzyskać tylko dane hello skojarzone z hello urządzenia, które były przechowywane w chmurze hello.

> [!WARNING]
> Dezaktywacja jest operacją trwałe i nie można cofnąć. O ile nie jest Resetuj domyślne toofactory dezaktywować urządzenie nie może zostać zarejestrowane hello usługi Menedżer StorSimple urządzenia.
>
> Fabryka Hello zresetować proces usuwania wszystkich danych hello, które były przechowywane lokalnie na urządzeniu. W związku z tym należy utworzyć migawkę chmury wszystkich danych przed dezaktywacją urządzenia. Ta migawka w chmurze pozwala toorecover hello wszystkich danych, aby w późniejszym terminie.

Po przeczytaniu tego samouczka, będą mieć możliwość:

* Dezaktywować urządzenie, a następnie usuń hello danych.
* Dezaktywować urządzenie i zachowywanie danych hello.

> [!NOTE]
> Przed dezaktywacją urządzenia fizycznego StorSimple lub urządzenia chmury zatrzymać lub usunąć klientów i hosty, które są zależne od tego urządzenia.


## <a name="deactivate-and-delete-data"></a>Dezaktywuj i usuwanie danych

Jeśli planuje się usuwanie urządzeń hello całkowicie i nie ma danych hello tooretain na urządzeniu hello, następnie wykonaj następujące kroki hello.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello urządzenia i delete hello danych

1. Przed dezaktywacją urządzenia, musisz usunąć wszystkie hello wolumin kontenerów (i woluminy hello) skojarzone z urządzeniem hello. Kontenery woluminów można usunąć tylko po usunięciu hello skojarzonych kopii zapasowych.

    > [!NOTE]
    > Przed dezaktywacją urządzenia fizycznego StorSimple lub urządzenia chmury, upewnij się, że dane hello z kontenera woluminów hello usunięte faktycznie są usuwane z urządzenia hello. Można monitorować hello chmury zużycie wykresów i po wyświetleniu użycia chmury hello upuść z powodu hello kopii zapasowych, które zostały usunięte, następnie można przystąpić toodeactivate hello urządzenia. Dezaktywacja urządzenia hello przed tej listy występuje, hello danych jest skrętki na koncie magazynu hello i zostały naliczone opłaty.

2. Dezaktywować urządzenie hello w następujący sposób:
   
   1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**. W hello **urządzeń** bloku, wybierz hello urządzenia mają toodeactivate, kliknij prawym przyciskiem myszy, a następnie kliknij **Dezaktywuj**.

        ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. W hello **Dezaktywuj** wpisz tooconfirm nazwy urządzenia hello bloku, a następnie kliknij przycisk **Dezaktywuj**. Witaj Dezaktywuj uruchamia proces i zajmuje kilka minut toocomplete.

        ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Po dezaktywacji możesz całkowicie usunąć urządzenie hello. Usuwanie urządzenia spowoduje usunięcie jej z listy hello usługi toohello podłączonych urządzeń. Usługa Hello można zarządzać już hello usunąć urządzenia. Użyj hello następujące kroki toodelete hello urządzenia:
   
   1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**. W hello **urządzeń** bloku, wybierz hello dezaktywowane urządzenia mają toodelete, kliknij prawym przyciskiem myszy, a następnie kliknij **usunąć**.

        ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. W hello **usunąć** wpisz tooconfirm nazwy urządzenia hello bloku, a następnie kliknij przycisk **usunąć**. Usuwanie Hello zajmuje kilka minut toocomplete.

        ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Po usunięciu hello jest zostało ukończone pomyślnie, zostanie wyświetlony. Lista urządzeń Hello aktualizuje również tooreflect hello usunięcia.

## <a name="deactivate-and-retain-data"></a>Dezaktywuj i Zachowaj dane

Jeśli chcą usuwania urządzenia hello, ale tooretain hello danych, wypełnij hello następujące kroki:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate urządzenia i zachowywanie danych hello
1. Dezaktywowanie hello urządzenia. Witaj wszystkie kontenery woluminów i pozostają migawki hello hello urządzenia.
   
   1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**. W hello **urządzeń** bloku, wybierz hello urządzenia mają toodeactivate, kliknij prawym przyciskiem myszy, a następnie kliknij **Dezaktywuj**.

         ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. W hello **Dezaktywuj** wpisz tooconfirm nazwy urządzenia hello bloku, a następnie kliknij przycisk **Dezaktywuj**. Witaj Dezaktywuj uruchamia proces i zajmuje kilka minut toocomplete.

         ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Możesz teraz w trybie Failover hello kontenery woluminów i hello skojarzone migawki. Procedur można przejść za[trybu Failover i odzyskiwania po awarii dla urządzenia StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. Po dezaktywacji i trybu failover można całkowicie usunąć urządzenie hello. Usuwanie urządzenia spowoduje usunięcie jej z listy hello usługi toohello podłączonych urządzeń. Usługa Hello można zarządzać już hello usunąć urządzenia. urządzenie hello toodelete, pełną hello następujące kroki:
   
   1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**. W hello **urządzeń** bloku, wybierz hello dezaktywowane urządzenia mają toodelete, kliknij prawym przyciskiem myszy, a następnie kliknij **usunąć**.

       ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. W hello **usunąć** wpisz tooconfirm nazwy urządzenia hello bloku, a następnie kliknij przycisk **usunąć**. Usuwanie Hello zajmuje kilka minut toocomplete.

       ![Dezaktywuj urządzenia StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Po usunięciu hello jest zostało ukończone pomyślnie, zostanie wyświetlony. Lista urządzeń Hello aktualizuje również tooreflect hello usunięcia.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Dezaktywuj i usuń urządzenia chmury

Chmura urządzenia StorSimple dezaktywacji z portalu hello cofa alokację i usuwa hello maszyny wirtualnej i zasoby hello utworzone podczas inicjowania jej obsługi. Po dezaktywacji urządzenia chmury hello, nie można go przywrócić tooits poprzedniego stanu.

![Dezaktywuj urządzenia StorSimple chmury](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Dezaktywacja powoduje hello następujące akcje:

* Witaj urządzenia chmury StorSimple jest usuwany z hello usługi.
* Maszyna wirtualna Hello na powitania urządzenia chmury StorSimple została usunięta.
* Witaj dysku systemu operacyjnego i dyski danych utworzone dla urządzenia chmury StorSimple hello są usuwane.
* Usługa hostowana Hello i sieci wirtualnej, które zostały utworzone podczas inicjowania obsługi zostaną zachowane. Jeśli nie używasz te jednostki, należy usunąć je ręcznie.
* Utworzone przez hello urządzenia chmury StorSimple migawki w chmurze są zachowywane.

Po dezaktywacji urządzenia chmury hello, należy ją usunąć z listy hello urządzeń. Wybierz hello dezaktywować urządzenie, kliknij prawym przyciskiem myszy, a następnie kliknij **usunąć**. StorSimple powiadamia po hello urządzenia zostanie usunięta i hello listy urządzeń.

## <a name="next-steps"></a>Następne kroki

* toorestore hello domyślne toofactory dezaktywować urządzenie znajduje się zbyt[przywrócić ustawienia domyślne toofactory urządzenia hello](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Aby uzyskać pomoc techniczną [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* więcej informacji o toolearn, jak hello toouse usługi Menedżer StorSimple urządzenia go za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

