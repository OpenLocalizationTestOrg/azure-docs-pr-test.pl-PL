---
title: "Tryb urządzenia StorSimple aaaChange | Dokumentacja firmy Microsoft"
description: "Zawiera opis tryby urządzenia StorSimple hello i jak toouse środowiska Windows PowerShell dla StorSimple toochange hello tryb urządzenia."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Zmień tryb urządzenia hello na urządzeniu StorSimple

Ten artykuł zawiera krótki opis hello różnych trybach, w których może działać urządzenia StorSimple. Urządzenia StorSimple może działać w trzech trybów: Normalny, obsługi i odzyskiwania.

Po przeczytaniu tego artykułu, oznacza to:

* Jakie są tryby urządzenia StorSimple hello
* Jak toofigure limit trybu hello urządzenia StorSimple znajduje się w
* Jak toochange w trybie normalnym toomaintenance i *na odwrót*

Witaj powyżej zadania związane z zarządzaniem można wykonać tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia StorSimple.

## <a name="about-storsimple-device-modes"></a>Temat trybów urządzenia StorSimple

Urządzenia StorSimple może działać w trybie normalnym, konserwacji lub odzyskiwania. Każdy z tych trybów krótko opisano poniżej.

### <a name="normal-mode"></a>Tryb normalny

To jest zdefiniowany jako hello normalnym trybem operacyjnych urządzenie StorSimple w pełni skonfigurowany. Domyślnie urządzenia powinny być w trybie normalnym.

### <a name="maintenance-mode"></a>Tryb konserwacji

Czasami hello urządzenia StorSimple może być konieczne toobe przełączony w tryb konserwacji. Ten tryb umożliwia tooperform konserwacji na urządzeniu hello i zainstaluj destrukcyjne aktualizacje, takie jak te dotyczące toodisk oprogramowania układowego.

Hello system można umieścić w tryb konserwacji tylko przy użyciu hello środowiska Windows PowerShell dla urządzenia StorSimple. Wszystkie żądania We/Wy są wstrzymane w tym trybie. Usług takich jak trwałej pamięci (NVRAM) lub usługa klastrowania hello również zostały zatrzymane. Zarówno kontrolery hello są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb. Po wyjściu z trybu konserwacji hello, wszystkie usługi hello wznowi i powinna być w dobrej kondycji. Może to potrwać kilka minut.

> [!NOTE]
> **Tryb konserwacji jest obsługiwana tylko na urządzeniu działa prawidłowo. Nie jest obsługiwane na urządzeniu, w którym jednego lub obu kontrolerów hello nie działają.**


### <a name="recovery-mode"></a>Tryb odzyskiwania

Tryb odzyskiwania można określić jako "Tryb awaryjny dla systemu Windows z obsługą sieci". Tryb odzyskiwania angażujący zespołu Microsoft Support hello oraz pozwala tooperform diagnostyki w systemie hello. podstawowym celem Hello trybu odzyskiwania jest dzienniki systemu hello tooretrieve.

System przechodzi do trybu odzyskiwania, należy skontaktować się Microsoft Support dalsze czynności. Aby uzyskać więcej informacji, przejdź zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).

> [!NOTE]
> **Nie można umieścić hello urządzenia w trybie odzyskiwania. Jeśli urządzenie hello jest w złym stanie, tryb odzyskiwania próbuje tooget hello urządzenia do stanu, w której personel firmy Microsoft Support można sprawdzić jego.**

## <a name="determine-storsimple-device-mode"></a>Określić tryb urządzenia StorSimple

#### <a name="toodetermine-hello-current-device-mode"></a>bieżący tryb urządzenia toodetermine hello

1. Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Sprawdź komunikat transparentu hello w menu konsoli szeregowej hello hello urządzenia. Ten komunikat oznacza jawnie, czy urządzenie hello jest w trybie konserwacji lub odzyskiwania. Jeśli wiadomość hello nie zawiera żadnych określonych informacji dotyczących trybu systemu toohello, urządzenie hello jest w trybie normalnym.

## <a name="change-hello-storsimple-device-mode"></a>Zmień tryb urządzenia StorSimple hello

Możesz umieścić hello urządzenia StorSimple do obsługi trybu (w trybie normalnym) tooperform konserwacji lub aktualizacji trybu konserwacji. Wykonaj następujące procedury tooenter lub zakończenia trybu konserwacji hello.

> [!IMPORTANT]
> Przed wprowadzeniem tryb konserwacji, sprawdź, czy zarówno kontrolery urządzeń są dobrej kondycji, uzyskując dostęp do hello **ustawienia urządzenia > kondycji sprzętu** dla urządzenia w portalu Azure hello. Jeśli jeden lub oba kontrolerów hello nie jest dobra, skontaktuj się z Microsoft Support hello następnych kroków. Aby uzyskać więcej informacji, przejdź zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).
 

#### <a name="tooenter-maintenance-mode"></a>Tryb konserwacji tooenter

1. Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**. jest Hello domyślne hasło: `Password1`.
3. Wpisz w wierszu polecenia hello 
   
    `Enter-HcsMaintenanceMode`
4. Pojawi się komunikat ostrzegawczy informujący, że tryb konserwacji będzie zakłócać wszystkich żądań We/Wy i sever hello połączenia toohello portalu Azure i zostanie wyświetlony monit o potwierdzenie. Typ **Y** tooenter tryb konserwacji.
5. Zarówno kontrolery zostanie uruchomiony ponownie. Po zakończeniu ponownego uruchomienia hello transparent konsoli szeregowej hello będzie wskazująca, że urządzenie hello jest w trybie konserwacji. Poniżej pokazano przykładowe dane wyjściowe.

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a>Tryb konserwacji tooexit

1. Zaloguj się na konsoli szeregowej urządzenia toohello. Sprawdź z hello komunikat transparentu, że urządzenie jest w trybie konserwacji.
2. Witaj wiersza polecenia wpisz:
   
    `Exit-HcsMaintenanceMode`
3. Zostanie wyświetlony komunikat ostrzegawczy i komunikat potwierdzenia. Typ **Y** tooexit tryb konserwacji.
4. Zarówno kontrolery zostanie uruchomiony ponownie. Po zakończeniu ponownego uruchomienia hello hello transparent konsoli szeregowej wskazuje, że urządzenie tym hello jest w trybie normalnym. Poniżej pokazano przykładowe dane wyjściowe.

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[stosowania aktualizacji tryb normalny i konserwacja](storsimple-update-device.md) na urządzeniu StorSimple.

