---
title: "aaaChange haseł za pomocą Menedżera urządzeń StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello toochange usługi Menedżer StorSimple hasła administratora StorSimple Snapshot Manager i urządzeń."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Użyj toochange usługi Menedżer StorSimple hello hasła StorSimple
## <a name="overview"></a>Omówienie
Witaj klasycznego portalu Azure **Konfiguruj** strona zawiera wszystkie parametry hello urządzenia, które można skonfigurować na urządzeniu StorSimple, który jest zarządzany przez usługę Menedżer StorSimple. W tym samouczku opisano, jak używasz hello **Konfiguruj** strony toochange administratora urządzenia lub hasło programu StorSimple Snapshot Manager.

## <a name="change-hello-device-administrator-password"></a>Hasło administratora urządzenia hello zmiany
Gdy używasz urządzenia StorSimple hello tooaccess interfejsu programu Windows PowerShell jest wymagane tooenter hasło administratora urządzenia. Po zarejestrowaniu hello pierwszego urządzenia StorSimple z usługą hello domyślne hasło dla tego interfejsu jest *Password1*. Dla bezpieczeństwa hello danych, są wymagane toochange hasła przy hello koniec hello procesu rejestracji. Nie można zamknąć z hello procesu rejestracji, bez zmiany hasła. Aby uzyskać więcej informacji, zobacz [krok 3: Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

następnie można zmienić hasło Hello najpierw ustawione za pośrednictwem interfejsu programu Windows PowerShell hello podczas rejestracji, hello klasycznego portalu Azure. Wykonaj powitania po hasło administratora urządzenia hello toochange czynności.

#### <a name="toochange-hello-device-administrator-password"></a>hasło administratora urządzenia hello toochange
1. W portalu klasycznym powitania kliknij **urządzeń** > **Konfiguruj** dla danego urządzenia.
2. Przewiń w dół toohello **hasło administratora urządzenia** sekcji. Podaj hasło administratora, który zawiera z 8 znaków too15. Hello hasło musi zawierać kombinację 3 lub więcej znaków wielkie litery, małe litery, liczbowych i specjalnych.
3. Potwierdź hasło hello.
4. Kliknij przycisk **zapisać** u dołu hello hello strony.

należy teraz zaktualizować hasło administratora urządzenia Hello. Można użyć tego interfejsu programu Windows PowerShell hello tooaccess zmodyfikowane hasło.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Zmień hasło programu StorSimple Snapshot Manager hello
Oprogramowanie StorSimple Snapshot Manager znajduje się na hoście z systemem Windows i pozwala administratorom tworzenie kopii zapasowych toomanage urządzenia StorSimple w formie hello lokalne i migawki w chmurze.

Podczas konfigurowania urządzenia StorSimple Snapshot Manager, zostanie wyświetlony monit tooprovide hello IP urządzenia tooauthenticate adres i hasło urządzenia magazynującego. To hasło jest już skonfigurowane za pośrednictwem interfejsu programu Windows PowerShell hello. Aby uzyskać więcej informacji, zobacz [krok 3: Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

następnie można zmienić za pośrednictwem klasycznego portalu hello hasło Hello najpierw ustawione za pośrednictwem interfejsu programu Windows PowerShell hello podczas rejestracji. Wykonaj powitania po hasło programu StorSimple Snapshot Manager hello toochange czynności.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>hasło programu StorSimple Snapshot Manager hello toochange
1. W portalu klasycznym powitania kliknij **urządzeń** > **Konfiguruj** dla danego urządzenia.
2. Przewiń w dół toohello **StorSimple Snapshot Manager** sekcji. Wprowadź hasło składające się z 14 do 15 znaków. Upewnij się, że to hasło hello zawiera kombinację 3 lub więcej znaków wielkie litery, małe litery, liczbowych i specjalnych.
3. Potwierdź hasło hello.
4. Kliknij przycisk **zapisać** u dołu hello hello strony.

hasło programu StorSimple Snapshot Manager Hello teraz powinny zostać uaktualnione.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-security.md).
* Dowiedz się więcej o [modyfikowanie konfiguracji urządzenia](storsimple-modify-device-config.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

