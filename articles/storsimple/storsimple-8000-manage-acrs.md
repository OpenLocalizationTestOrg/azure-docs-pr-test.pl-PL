---
title: "aaaManage rekordy kontroli dostępu w StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak kontroli dostępu toouse rekordy hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello toodetermine (ACRs)."
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
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Użyj rekordy kontroli dostępu toomanage usługi Menedżer StorSimple hello

## <a name="overview"></a>Omówienie
Rekordy kontroli dostępu (ACRs) pozwalają toospecify hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello. ACRs są ustawiane tooa określonego woluminu i zawierają hello iSCSI nazwy kwalifikowane (nazw IQN) hello hostów. Gdy host podejmie próbę tooconnect tooa woluminu, hello urządzenia sprawdza powitalne ACR skojarzone z tym woluminie nazwy IQN hello i jeśli istnieje dopasowanie, a następnie hello jest nawiązywane połączenie. Witaj rekordy kontroli dostępu w hello **konfiguracji** sekcji z bloku usługi Menedżer StorSimple urządzenia wyświetlić wszystkie rekordy kontroli dostępu hello z hello odpowiadającego nazw IQN hello hostów.

W tym samouczku opisano następujące typowe zadania związane z ACR hello:

* Dodaj rekord kontroli dostępu
* Edytuj rekord kontroli dostępu
* Usuń rekord kontroli dostępu

> [!IMPORTANT]
> * Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.
> * Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.

## <a name="get-hello-iqn"></a>Pobierz hello IQN

Wykonaj następujące kroki tooget hello IQN hosta z systemem Windows z systemem Windows Server 2012 hello.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Dodaj rekord kontroli dostępu
Użyj hello **konfiguracji** części hello Menedżera urządzeń StorSimple usługi bloku tooadd ACRs. Zazwyczaj co ACR zostanie skojarzony z jednego woluminu.

Wykonaj następujące kroki tooadd ACR hello.

#### <a name="tooadd-an-acr"></a>tooadd ACR

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.
2. W hello **rekordy kontroli dostępu** bloku, kliknij przycisk **+ Dodaj ACR**.

    ![Kliknij przycisk Dodaj ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. W hello **dodać ACR** bloku hello następujące kroki:

    1. Podaj nazwę dla rekordu ACR.
    
    2. Podaj nazwę IQN hello danego hosta systemu Windows Server, w obszarze **iSCSI Nazwa inicjatora (IQN)**.

    3. Kliknij przycisk **Dodaj** toocreate hello ACR.

        ![Kliknij przycisk Dodaj ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Witaj nowo dodanych ACR będą wyświetlane na powitania Tabelaryczny spis ACRs.

    ![Kliknij przycisk Dodaj ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Edytuj rekord kontroli dostępu
Użyj hello **konfiguracji** części hello Menedżera urządzeń StorSimple usługi bloku tooedit ACRs.

> [!NOTE]
> Zalecane jest zmodyfikowanie tych ACRs, które nie są obecnie w użyciu. tooedit ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.

Wykonaj następujące kroki tooedit ACR hello.

#### <a name="tooedit-an-access-control-record"></a>tooedit rekord kontroli dostępu
1.  Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/createacr1.png)

2. W hello tabelarycznej listę rekordy kontroli dostępu hello, kliknij i zaznacz hello ACR, że chcesz toomodify.

    ![Edytuj rekordy kontroli dostępu](./media/storsimple-8000-manage-acrs/editacr1.png)

3. W hello **rekord kontroli dostępu edycji** bloku, podaj inny host tooanother odpowiedniego IQN.

    ![Edytuj rekordy kontroli dostępu](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Kliknij pozycję **Zapisz**. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. 

    ![Edytuj rekordy kontroli dostępu](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Użytkownik jest powiadamiany o zaktualizowaniu hello ACR. Lista tabelarycznym Hello aktualizuje również tooreflect hello zmiany.

   
## <a name="delete-an-access-control-record"></a>Usuń rekord kontroli dostępu
Użyj hello **konfiguracji** części hello Menedżera urządzeń StorSimple usługi bloku toodelete ACRs.

> [!NOTE]
> Można usunąć tylko ACRs, które nie są obecnie w użyciu. toodelete ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.

Wykonaj hello następujące kroki toodelete rekord kontroli dostępu.

#### <a name="toodelete-an-access-control-record"></a>toodelete rekord kontroli dostępu
1.  Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/createacr1.png)

2. W hello tabelarycznej listę rekordy kontroli dostępu hello, kliknij i zaznacz hello ACR, że chcesz toodelete.

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke i wybierz **usunąć**.

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Po wyświetleniu monitu o potwierdzenie, przejrzyj informacje hello, a następnie kliknij przycisk **usunąć**.

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Użytkownik jest powiadamiany o zakończeniu hello usunięcia. Tworzenie listy tabelarycznym Hello jest zaktualizowane tooreflect hello usunięcia.

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-8000-manage-volumes-u2.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

