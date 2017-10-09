---
title: "aaaManage rekordy kontroli dostępu dla tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak kontroli dostępu toomanage rekordy toodetermine (ACRs), których hostów można połączyć tooa woluminu na powitania tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>Toomanage StorSimple za pomocą Menedżera urządzeń rekordy kontroli dostępu dla tablicy wirtualnego StorSimple

## <a name="overview"></a>Omówienie

Rekordy kontroli dostępu (ACRs) pozwalają toospecify hosty, które mogą się łączyć tooa woluminu na powitania tablicy wirtualnego StorSimple (znanej także jako hello lokalnej urządzenia wirtualnego StorSimple). ACRs są ustawiane tooa określonego woluminu i zawierają hello iSCSI nazwy kwalifikowane (nazw IQN) hello hostów. Gdy host podejmie próbę tooconnect tooa woluminu, hello urządzenia sprawdza hello ACR skojarzone z tym woluminie dla nazwy IQN hello i jeśli istnieje dopasowanie, hello połączenie zostanie nawiązane. Witaj **rekordy kontroli dostępu** bloku w hello **konfiguracji** sekcji usługi Menedżer urządzeń wyświetla wszystkie rekordy kontroli dostępu hello hello odpowiadającego nazw IQN hello hostów.

![Zarządzanie rekordami kontroli dostępu](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

W tym samouczku opisano następujące typowe zadania związane z ACR hello:

* Pobierz hello IQN
* Dodaj rekord kontroli dostępu
* Edytuj rekord kontroli dostępu
* Usuń rekord kontroli dostępu

> [!IMPORTANT]
> 
> * Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.
> * Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.


## <a name="get-hello-iqn"></a>Pobierz hello IQN

Wykonaj następujące kroki tooget hello IQN hosta z systemem Windows z systemem Windows Server 2012 hello.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Dodaj ACR

Możesz użyć **rekordy kontroli dostępu** bloku w hello **konfiguracji** sekcji z tooadd usługi Menedżer StorSimple urządzenia ACRs. Zazwyczaj należy skojarzyć jedną ACR z jednego woluminu.

Informacji o kojarzeniu ACR z woluminem, przejdź zbyt[Dodaj wolumin](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.


Wykonaj następujące kroki tooadd ACR hello.

#### <a name="tooadd-an-acr"></a>tooadd ACR

1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.
2. W hello **rekordy kontroli dostępu** bloku, kliknij przycisk **Dodaj**.
3. W hello **dodać ACR** bloku hello następujące:
   
    1. Wypełnij pole **Nazwa** dla rekordu ACR.
    
    2. W obszarze **Nazwa inicjatora iSCSI**, podaj hello nazwę IQN hosta z systemem Windows. Witaj tooget IQN hosta z systemem Windows Server, hello następujące:
   
    3. Uruchom inicjatora iSCSI firmy Microsoft hello na hoście z systemem Windows. W oknie właściwości inicjatora iSCSI hello, na powitania **konfiguracji** karcie zaznacz i skopiuj ciąg hello z hello **Nazwa inicjatora** pola.
    Wklej ten ciąg hello **IQN** w hello **dodać ACR** bloku.
   
    6. Kliknij przycisk **Dodaj** tooadd hello ACR.  
   
        ![Dodaj rekordy kontroli dostępu](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. Witaj tabelarycznej listę jest zaktualizowane tooreflect tego dodatku.

## <a name="edit-an-acr"></a>Edytuj ACR

Użyj hello **rekordy kontroli dostępu** bloku w hello **konfiguracji** sekcji usługi Menedżera urządzeń w hello ACRs tooedit portalu Azure.

> [!NOTE]
> Nie należy modyfikować ACR, który jest aktualnie używany. tooedit ACR skojarzony z woluminem, który jest aktualnie używana, należy najpierw wziąć hello woluminu w trybie offline.


Wykonaj następujące kroki tooedit ACR hello.

#### <a name="tooedit-an-acr"></a>tooedit ACR

1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** sekcji **rekordy kontroli dostępu**.
2. W hello **rekordy kontroli dostępu** bloku z hello Tabelaryczny spis hello rekordy kontroli dostępu, kliknij dwukrotnie hello ACR, że chcesz toomodify.
3. W hello **rekordy kontroli dostępu do edycji** bloku hello następujące:
   
    1. Podaj hello IQN dla hello ACR.
   
    2. Kliknij przycisk **zapisać** u góry hello toosave bloku hello hello zmodyfikowane ACR. Zostanie wyświetlony powitania po komunikat potwierdzenia:
   
        ![Edytuj rekordy kontroli dostępu](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Usuń rekord kontroli dostępu

Użyj hello **konfiguracji** strony w hello ACRs toodelete portalu Azure.

> [!NOTE]
> 
> * Nie należy usuwać ACR, który jest aktualnie używany. toodelete ACR skojarzony z woluminem, który jest aktualnie używana, należy najpierw wziąć hello woluminu w trybie offline.
> * Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.


Wykonaj hello następujące kroki toodelete rekord kontroli dostępu.

#### <a name="toodelete-an-access-control-record"></a>toodelete rekord kontroli dostępu

1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** sekcji **rekordy kontroli dostępu**.

2. W hello **rekordy kontroli dostępu** bloku z hello Tabelaryczny spis hello rekordy kontroli dostępu, kliknij dwukrotnie hello ACR, że chcesz toodelete.

3. W bloku rekordów hello edycji dostępu formantu, kliknij **usunąć**.
   
    ![Usuń ACRS](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **usunąć** toocontinue z hello usunięcia. Tworzenie listy tabelarycznym Hello jest zaktualizowane tooreflect hello usunięcia.
   
   ![Komunikat ostrzegawczy](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [Dodawanie woluminów i konfigurowanie ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

