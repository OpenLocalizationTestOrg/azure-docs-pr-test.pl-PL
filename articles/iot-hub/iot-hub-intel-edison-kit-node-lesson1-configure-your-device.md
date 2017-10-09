---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie Intel Edison do pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino Konfigurowanie, Połącz arduino toopc, arduino Instalatora, arduino tablicy"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Konfigurowanie sieci Edison Intel
## <a name="what-you-will-do"></a>Będzie wykonywać
Konfigurowanie Intel Edison do użycia po raz pierwszy przez łączenie tablicy hello, włączanie go i instalowanie konfiguracji narzędzia tooyour pulpitu systemu operacyjnego tooflash Edison w oprogramowaniu układowym, ustaw hasło i podłącz go tooWi-Fi. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak płycie tooassemble Edison i włączenie go w górę.
* Jak tooflash Edison oprogramowania układowego, ustaw hasło i połączenia sieci Wi-Fi.

## <a name="what-you-need"></a>Co jest potrzebne
toocomplete tej operacji, należy po części z Twojej firmy Intel Edison Starter Kit hello:

* Moduł Intel® Edison
* Karty rozszerzeń Arduino
* Paski rozdzielacza lub śruby zawarte w pakiecie hello, w tym cztery zestawy śruby i tworzywa odstępników i dwie śruby toofasten hello modułu toohello rozszerzenia tablicy.
* TooType Micro B kabla A USB
* Zasilacz prądu (DC). Zasilacza powinny być sklasyfikowane w następujący sposób:
  - 7-15V KONTROLERA DOMENY
  - Co najmniej 1500mA
  - numer pin center/wewnętrzny Hello powinna być bieguna dodatnie hello hello zasilania

  ![Elementy w zestawie początkowy](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Wymagane są również:

* Komputer z systemem Windows, Mac lub Linux.
* Połączenia bezprzewodowego tooconnect Edison do.
* Internet połączenia toodownload narzędzie konfiguracji.

## <a name="assemble-your-board"></a>Złóż tablicy

Ta sekcja zawiera kroki tooattach Intel® Edison modułu tooyour rozszerzenia tablicy.

1. Umieść hello Intel® Edison modułu w ramach konspektu hello białe na tablicy rozszerzenia, wyrównywanie hello luk w hello module z śruby hello na powitania rozszerzenia tablicy.

2. Naciśnij modułu hello poniżej słowa hello `What will you make?` dopóki uważasz, że bardzo proste.

   ![Złóż tablicy 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Użyj karty rozszerzeń toohello hello dwa szesnastkowych poziomie NTS (zawarte w pakiecie hello) toosecure hello modułu.

   ![Złóż tablicy 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Wstaw śruby w jednej z czterech luk rogu hello na powitania rozszerzenia tablicy. Skręcenie i zwiększyć jedną hello białe plastikowe odstępników na powitania gwintowanym.

   ![Złóż tablicy 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Powtórz te czynności dla hello innych odstępników trzy rogu.

   ![Złóż tablicy 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Teraz budowy tablicy.

   ![złożony tablicy](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Włącz Edison

1. Dołącz hello zasilania.

   ![Podłącz zasilacz](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Zielona LED (oznaczony DS1 na powitania karty rozszerzeń Arduino *) powinien podświetlony i pozostać podświetlone.

3. Poczekaj na jedną minutę na powitania tablicy toofinish rozruch.

   > [!NOTE]
   > Jeśli nie masz zasilacz kontrolera domeny, można nadal zasilania hello tablicy za pośrednictwem portu USB. Zobacz `Connect Edison tooyour computer` sekcji, aby uzyskać szczegółowe informacje. Włączanie tablicy w ten sposób może spowodować nieprzewidywalne zachowanie z tablicy, szczególnie w przypadku, gdy przy użyciu sieci Wi-Fi lub zwiększają motors.

## <a name="connect-edison-tooyour-computer"></a>Podłącz komputer tooyour Edison

1. Przełącz dół mikroprzełącznika hello kierunku Witaj dwie micro portów USB, dzięki czemu Edison jest w trybie urządzenia. Różnice między trybu urządzenia ani hosta, odwołanie [tutaj](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Przełącz mikroprzełącznika hello w dół](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Podłącz kabel USB micro hello do portu USB micro najwyższego hello.

   ![Górny micro portu USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Plug hello drugiej, kabel USB do komputera.

   ![Komputer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Będzie wiadomo, że tablicy jest w pełni zainicjowany, gdy komputer instaluje nowy dysk (podobne jak w przypadku Wstawianie karta SD do komputera).

## <a name="download-and-run-hello-configuration-tool"></a>Pobierz i uruchom narzędzie konfiguracji hello
Pobierz najnowsze narzędzia konfiguracji hello z [to łącze](https://software.intel.com/en-us/iot/hardware/edison/downloads) kategorii hello `Installers` nagłówka. Wykonaj hello narzędzia i postępuj zgodnie z jego na ekranie instrukcjami, klikając przycisk Dalej, w razie potrzeby

### <a name="flash-firmware"></a>Oprogramowanie układowe Flash
1. Na powitania `Set up options` kliknij `Flash Firmware`.
2. Wybierz hello tooflash obrazu na tablicy, wykonując jedną z następujących hello:
   - toodownload i flash tablicy o hello najnowszego oprogramowania układowego obraz dostępne z firmy Intel, wybierz `Download hello latest image version xxxx`.
   - Wybierz tablicy z obrazem, który został zapisany już na komputerze, tooflash `Select hello local image`. Przeglądaj tooand hello wybierz obraz ma tooflash tooyour tablicy.
3. Narzędzie Instalatora Hello podejmie tooflash tablicy. cały proces miga Hello może trwać too10 minut.

### <a name="set-password"></a>Ustaw hasło
1. Na powitania `Set up options` kliknij `Enable Security`.
2. Można ustawić niestandardową nazwę tablicy Intel® Edison. Jest to opcjonalne.
3. Wpisz hasło do tablicy, a następnie kliknij przycisk `Set password`.
4. Oznacz hello hasła, które jest później używany w dół.

### <a name="connect-wi-fi"></a>Połączenia sieci Wi-Fi
1. Na powitania `Set up options` kliknij `Connect Wi-Fi`. Poczekaj zapasowej minutę tooone jako użytkownika skanowania komputera dostępnych sieci Wi-Fi.
2. Z hello `Detected Networks` listy rozwijanej wybierz sieci.
3. Z hello `Security` listy rozwijanej, wybierz hello sieci typu zabezpieczeń.
4. Udostępnić informacje logowania i hasło, a następnie kliknij przycisk `Configure Wi-Fi`.
5. Oznacz dół hello adres IP, który jest później używany.

> [!NOTE]
> Upewnij się, że Edison jest połączonych toohello sam sieci jako komputera. Komputer łączy tooyour Edison przy użyciu adresu IP hello.

Gratulacje! Pomyślnie skonfigurowano Edison.

## <a name="summary"></a>Podsumowanie
W tym artykule kiedy znasz już jak tooassemble hello tablicy Edison, flash jego oprogramowania układowego, ustawienia hasła i podłącz go tooWi-Fi za pomocą narzędzia konfiguracji. Należy pamiętać, że powitalne LED jeszcze nie podświetlony. następne zadanie Hello jest tooinstall hello niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na Edison przykładowej aplikacji.

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia hello][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md