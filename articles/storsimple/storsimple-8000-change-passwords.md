---
title: "aaaChange haseł StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello toochange usługi Menedżer StorSimple urządzenia StorSimple Snapshot Manager i urządzeń hasła administratora."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Użyj toochange usługi Menedżer StorSimple urządzenia hello hasła StorSimple

## <a name="overview"></a>Omówienie
Witaj w portalu Azure **ustawienia urządzenia** opcja zawiera wszystkie parametry hello urządzenia, które można skonfigurować na urządzeniu StorSimple, które jest zarządzane przez usługę Menedżera urządzeń StorSimple. W tym samouczku opisano, jak używasz hello **zabezpieczeń** opcję w obszarze **ustawienia urządzenia** toochange administratora urządzenia lub hasło programu StorSimple Snapshot Manager.

## <a name="change-hello-device-administrator-password"></a>Hasło administratora urządzenia hello zmiany
Gdy używasz urządzenia StorSimple hello tooaccess interfejsu programu Windows PowerShell jest wymagane tooenter hasło administratora urządzenia. Po zarejestrowaniu hello pierwszego urządzenia StorSimple z usługą hello domyślne hasło dla tego interfejsu jest *Password1*. Dla bezpieczeństwa hello danych, są wymagane toochange hasła przy hello koniec hello procesu rejestracji. Nie można zamknąć z hello procesu rejestracji, bez zmiany hasła. Aby uzyskać więcej informacji, zobacz [krok 3: Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

hasło Hello najpierw ustawione za pośrednictwem interfejsu programu Windows PowerShell hello podczas rejestracji można później zmienić za pomocą hello portalu Azure. Wykonaj powitania po hasło administratora urządzenia hello toochange czynności.

#### <a name="toochange-hello-device-administrator-password"></a>hasło administratora urządzenia hello toochange
1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**.

2. Z hello tabelarycznej listę urządzeń, wybierz i kliknij hello urządzenie, którego hasło ma toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. W hello **ustawienia** bloku Przejdź zbyt**ustawienia urządzenia > zabezpieczeń**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **hasło** hasło administratora urządzenia hello toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. W hello **hasło** bloku, który zawiera z 8 znaków too15 hasło administratora. Hello hasło musi zawierać kombinację 3 lub więcej znaków wielkie litery, małe litery, liczbowych i specjalnych.

6. Potwierdź hasło hello.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

należy teraz zaktualizować hasło administratora urządzenia Hello. Można użyć tego interfejsu programu Windows PowerShell hello tooaccess zmodyfikowane hasło.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Ustaw hasło programu StorSimple Snapshot Manager hello
Oprogramowanie StorSimple Snapshot Manager znajduje się na hoście z systemem Windows i pozwala administratorom tworzenie kopii zapasowych toomanage urządzenia StorSimple w formie hello lokalne i migawki w chmurze.

Podczas konfigurowania urządzenia StorSimple Snapshot Manager, zostanie wyświetlony monit tooprovide hello IP urządzenia tooauthenticate adres i hasło urządzenia magazynującego.

Możesz ustawić lub zmienić hasło hello StorSimple Snapshot Manager za pośrednictwem hello portalu Azure. Wykonaj następujące kroki tooset hello, lub zmień hasło programu StorSimple Snapshot Manager hello.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>hasło programu StorSimple Snapshot Manager hello tooset
1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**.

2. Z hello tabelarycznej listę urządzeń, wybierz i kliknij urządzenie hello którego hasło programu StorSimple Snapshot Manager mają tooset lub zmienić.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. W hello **ustawienia** bloku Przejdź zbyt**ustawienia urządzenia > zabezpieczeń**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **hasło** tooset lub zmień hasło programu StorSimple Snapshot Manager hello.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. W hello **hasło** bloku, wprowadź hasło składające się z 14 do 15 znaków. Upewnij się, że to hasło hello zawiera kombinację 3 lub więcej znaków wielkie litery, małe litery, liczbowych i specjalnych.

6. Potwierdź hasło hello.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

hasło programu StorSimple Snapshot Manager Hello teraz powinny zostać uaktualnione.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-8000-security.md).
* Dowiedz się więcej o [modyfikowanie konfiguracji urządzenia](storsimple-8000-modify-device-config.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

