---
title: "Connect Intel Edison (C) do Azure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie Intel Edison do pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino ustawienie nawiązać arduino komputerów, arduino Instalatora, arduino tablicy"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a>Konfigurowanie sieci Edison Intel
## <a name="what-you-will-do"></a>Będzie wykonywać
Konfigurowanie Intel Edison do użycia po raz pierwszy przez łączenie tablicy go podłączone do zasilania i instalacja narzędzia do konfiguracji pulpitu system operacyjny do flash Edison w oprogramowaniu układowym, ustaw hasło i połącz ją z sieci Wi-Fi. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak utworzyć Edison tablicy i włączenie go w górę.
* Jak flash Edison w oprogramowaniu układowym, ustaw hasło i połączenia sieci Wi-Fi.

## <a name="what-you-need"></a>Co jest potrzebne
Aby wykonać tę operację, potrzebne następujące elementy z Twojej firmy Intel Edison Starter Kit:

* Moduł Intel® Edison
* Karty rozszerzeń Arduino
* Paski rozdzielacza lub śruby zawarte w pakiecie, łącznie z dwóch śruby aby przyspieszyć modułu do karty rozszerzeń i cztery zestawy śruby i tworzywa odstępników.
* B Micro do kabla USB A typu
* Zasilacz prądu (DC). Zasilacza powinny być sklasyfikowane w następujący sposób:
  - 7-15V KONTROLERA DOMENY
  - Co najmniej 1500mA
  - Numer pin center/wewnętrzny powinien być bieguna dodatnie zasilania

  ![Elementy w zestawie początkowy](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Wymagane są również:

* Komputer z systemem Windows, Mac lub Linux.
* Połączenia bezprzewodowego Edison do nawiązania połączenia.
* Połączenia internetowego na pobieranie narzędzia do konfiguracji.

## <a name="assemble-your-board"></a>Złóż tablicy

Ta sekcja zawiera kroki, aby dołączyć modułu Intel® Edison do tablicy rozszerzenia.

1. Umieść modułu Intel® Edison w obrębie białe konspektu na tablicy rozszerzenia, wyrównywanie luk w module z śruby na tablicy rozszerzenia.

2. Naciśnij modułu poniżej słowa `What will you make?` dopóki uważasz, że bardzo proste.

   ![Złóż tablicy 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Użyj dwóch szesnastkowych poziomie NTS (uwzględniony w pakiecie) do zabezpieczania modułu do karty rozszerzeń.

   ![Złóż tablicy 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Wstaw śruby w jednym z luk narożników na tablicy rozszerzenia. Skręcenie i zwiększyć jedną białe plastikowe odstępników na śrubę.

   ![Złóż tablicy 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Powtórz dla innych odstępników trzy rogu.

   ![Złóż tablicy 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Teraz budowy tablicy.

   ![złożony tablicy](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Włącz Edison

1. Podłącz zasilania.

   ![Podłącz zasilacz](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Zielona LED (oznaczony DS1 na tablicy rozszerzenia Arduino *) powinien podświetlony i pozostać podświetlone.

3. Zaczekaj minutę dla tablicy ukończyć rozruch.

   > [!NOTE]
   > Jeśli nie masz zasilacz kontrolera domeny, można nadal zasilanie tablicy za pośrednictwem portu USB. Zobacz `Connect Edison to your computer` sekcji, aby uzyskać szczegółowe informacje. Włączanie tablicy w ten sposób może spowodować nieprzewidywalne zachowanie z tablicy, szczególnie w przypadku, gdy przy użyciu sieci Wi-Fi lub zwiększają motors.

## <a name="connect-edison-to-your-computer"></a>Łączenie się z komputerem Edison

1. Przełącz dół mikroprzełącznika kierunku dwóch micro portów USB, dzięki czemu Edison jest w trybie urządzenia. Różnice między trybu urządzenia ani hosta, odwołanie [tutaj](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Przełącz mikroprzełącznika w dół](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Podłącz kabel USB micro do górnej micro portu USB.

   ![Górny micro portu USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Podłącz drugi koniec kabla USB do komputera.

   ![Komputer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Będzie wiadomo, że tablicy jest w pełni zainicjowany, gdy komputer instaluje nowy dysk (podobne jak w przypadku Wstawianie karta SD do komputera).

## <a name="download-and-run-the-configuration-tool"></a>Pobierz i uruchom narzędzie konfiguracji
Pobierz najnowsze narzędzia konfiguracji z [to łącze](https://software.intel.com/en-us/iot/hardware/edison/downloads) kategorii `Installers` nagłówka. Wykonywanie narzędzia i postępuj zgodnie z jego na ekranie instrukcjami, klikając przycisk Dalej, w razie potrzeby

### <a name="flash-firmware"></a>Oprogramowanie układowe Flash
1. Na `Set up options` kliknij `Flash Firmware`.
2. Wybierz obraz do flash na tablicy, wykonując jedną z następujących czynności:
   - Aby pobrać i flash tablicy przy użyciu najnowszej dostępnej w sklepie Intel obrazu oprogramowania układowego, wybierz `Download the latest image version xxxx`.
   - Aby flash tablicy z obrazem, który został zapisany już na komputerze, wybierz `Select the local image`. Wyszukaj i wybierz obraz, który ma być flash do tablicy.
3. Narzędzie instalacji będzie podejmować próby flash tablicy. Cały proces miga może potrwać do 10 minut.

### <a name="set-password"></a>Ustaw hasło
1. Na `Set up options` kliknij `Enable Security`.
2. Można ustawić niestandardową nazwę tablicy Intel® Edison. Jest to opcjonalne.
3. Wpisz hasło do tablicy, a następnie kliknij przycisk `Set password`.
4. Oznacz hasła, które jest później używany w dół.

### <a name="connect-wi-fi"></a>Połączenia sieci Wi-Fi
1. Na `Set up options` kliknij `Connect Wi-Fi`. Poczekaj maksymalnie jedną minutę, co komputer szuka dostępnych sieci Wi-Fi.
2. Z `Detected Networks` listy rozwijanej wybierz sieci.
3. Z `Security` listy rozwijanej wybierz typ zabezpieczeń sieci.
4. Udostępnić informacje logowania i hasło, a następnie kliknij przycisk `Configure Wi-Fi`.
5. Zaznacz adres IP, który jest później używany.

> [!NOTE]
> Upewnij się, że Edison jest podłączony do sieci z komputera. Komputer łączy się z Edison przy użyciu adresu IP.

Gratulacje! Pomyślnie skonfigurowano Edison.

## <a name="summary"></a>Podsumowanie
W tym artykule kiedy znasz już sposobu łączenia tablicy Edison, flash jego oprogramowania układowego, ustawienia hasła i podłącz go do sieci Wi-Fi za pomocą narzędzia konfiguracji. Należy pamiętać, że jeszcze nie podświetlony LED. Następne zadanie jest Zainstaluj niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na Edison przykładowej aplikacji.

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md