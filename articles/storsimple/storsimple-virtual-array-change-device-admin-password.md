---
title: "hasło administratora urządzenia StorSimple wirtualnego tablicy aaaChange | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse albo hello portalu Azure lub interfejsu użytkownika sieci web tablicy wirtualnego StorSimple toochange hasło administratora urządzenia hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Zmień hasło administratora urządzenia StorSimple wirtualnego tablicy hello za pomocą Menedżera urządzeń StorSimple

## <a name="overview"></a>Omówienie

Gdy używasz tooaccess interfejsu programu Windows PowerShell hello hello tablicy wirtualnego StorSimple, są wymagane tooenter hasło administratora urządzenia. Gdy urządzenie StorSimple hello jest najpierw udostępnione i uruchomiony, jest hello domyślne hasło *Password1*. Dla bezpieczeństwa hello danych, hello domyślne hasło wygaśnie hello zalogowaniu się po raz pierwszy, a są toochange wymagane hasło.

Umożliwia także albo hello lokalnej sieci web interfejsu użytkownika lub hello Azure toochange portalu hello hasło administratora urządzenia w dowolnej chwili po wdrożeniu urządzenia hello w środowisku produkcyjnym. W tym artykule opisano każdy z tych procedur.

 ![Blok urządzeń](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Użyj hello Azure toochange portalu hello hasła

Wykonaj następujące kroki toochange hello hasło administratora urządzenia za pośrednictwem portalu Azure hello hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>hasło administratora urządzenia hello toochange za pośrednictwem hello portalu Azure

1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **zarządzania** kliknij **urządzeń**. Spowoduje to otwarcie hello **urządzeń** bloku, który zawiera listę wszystkich urządzeń wirtualnych tablicy StorSimple.

2. W hello **urządzeń** bloku, kliknij dwukrotnie urządzenie hello, który wymaga zmiany hasła.

3. W hello **ustawienia** bloku dla danego urządzenia, kliknij przycisk **zabezpieczeń**.

4. W hello **ustawienia zabezpieczeń** bloku hello następujące:
   
   1. Przewiń w dół toohello **hasło administratora urządzenia** sekcji. Podaj hasło administratora, który zawiera z 8 znaków too15.
   2. Potwierdź hasło hello.
   3. Kliknij przycisk **zapisać** u góry bloku hello hello.

hasło administratora urządzenia Hello jest już uaktualniona. Można użyć tego hasła zmodyfikowanych tooaccess hello urządzenia lokalnie.

![Blok ustawień zabezpieczeń](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Użyj hello lokalnej sieci web UI toochange hello hasła

Wykonaj następujące kroki toochange hello hasło administratora urządzenia za pośrednictwem lokalne powitania interfejsu użytkownika sieci web hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>hasło administratora urządzenia hello toochange za pośrednictwem lokalne powitania interfejsu użytkownika sieci web

1. W hello lokalnego interfejsu użytkownika sieci web, kliknij przycisk **konserwacji** > **zmiany hasła** dla danego urządzenia.
   
    ![Zmień password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Wprowadź hello **bieżące hasło**.
3. Podaj **nowe hasło**. Witaj hasło musi być co najmniej 8 znaków. Musi zawierać 3 z 4 poniżej hello: wielkie litery, małe litery, liczbowego i znaki specjalne.
   
    Należy pamiętać, że hasło nie może być hello tak samo jak hello ostatnie 24 haseł.
4. Wprowadź ponownie tooconfirm hasło hello go.
   
    ![Zmień Hasło2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. U dołu hello hello strony, kliknij przycisk **Zastosuj**. teraz zastosowano Hello nowe hasło. Jeśli zmiana hasła hello zakończy się niepowodzeniem, zostanie wyświetlony hello następujący błąd:
   
    ![Błąd hasła](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Po pomyślnej aktualizacji hasła hello, użytkownik jest powiadamiany. To hasło modyfikacji tooaccess hello urządzenia można następnie użyć lokalnie.


## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[administrowania tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

