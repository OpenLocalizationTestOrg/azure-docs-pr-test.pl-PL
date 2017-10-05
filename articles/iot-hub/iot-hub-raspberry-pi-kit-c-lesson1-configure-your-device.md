---
title: "Connect Raspberry pi (C) do Azure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Skonfiguruj malina Pi 3 dla pierwszego użycia i zainstalować system operacyjny Raspbian wolnego systemu operacyjnego, który jest zoptymalizowana pod kątem sprzętu malina Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspbian instalacji, pobierania raspbian sposób instalowania raspbian, ustawienia raspbian, malinowe pi instalacji raspbian, os instalacji malinowe pi, zainstaluj karty sd malinowe pi, malina pi łączenia, nawiązać łączności pi malinowe pi malinowe"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a>Konfigurowanie urządzenia
## <a name="what-you-will-do"></a>Będzie wykonywać
Konfigurowanie Pi do pierwszego użycia i zainstaluj system operacyjny Raspbian. Raspbian jest bezpłatna systemu operacyjnego, który jest zoptymalizowana pod kątem sprzętu malina Pi. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak zainstalować Raspbian na Pi.
* Jak zasilanie Pi przy użyciu kabla USB.
* Jak nawiązać Pi sieci za pomocą kabla Ethernet lub sieci bezprzewodowej.
* Jak dodać diodę LED do breadboard i podłącz go do Pi.

## <a name="what-you-need"></a>Co jest potrzebne
Aby wykonać tę operację, potrzebne następujące części z Twojej malina Pi 3 Starter Kit:

* Tablica malina Pi 3
* Karta microSD 16 GB
* 5 volt 2-amp zasilacz z stopy 6 micro kabla USB
* Breadboard
* Przewodów łącznika
* Ohm — 560 opornikiem
* Rozproszona LED 10 mm
* Kabla Ethernet

![Elementy w zestawie początkowy](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Wymagane są również:

* Połączenia przewodowe i bezprzewodowe pi nawiązać połączenie.
* USB-karty sieciowej lub mini SD na kartach SD Nagraj obraz systemu operacyjnego na karcie microSD.
* Komputer z systemem Windows, Mac lub Linux. Komputer jest używany do zainstalowania na karcie microSD Raspbian.
* Połączenie internetowe, aby pobrać niezbędne narzędzia i oprogramowania.

## <a name="install-raspbian-on-the-microsd-card"></a>Zainstaluj na karcie MicroSD Raspbian
Przygotuj karty microSD instalacji obrazu Raspbian.

1. Pobierz Raspbian.
   1. [Pobierz](https://www.raspberrypi.org/downloads/raspbian/) pliku zip o Joasia Raspbian z pikseli.
   2. Wyodrębnij obrazu Raspbian do folderu na komputerze.
2. Zainstaluj Raspbian karty microSD.
   1. [Pobierz](https://www.etcher.io) i zainstaluj narzędzie palnika karty Etcher SD.
   2. Uruchom Etcher i wybierz obraz Raspbian, który został wyodrębniony w kroku 1.
   3. Wybierz dysk karty microSD.
      Należy pamiętać, że Etcher może już wybrane poprawnego dysku.
   4. Kliknij przycisk **Flash** instalowanie Raspbian karty microSD.
   5. Karta microSD należy usunąć z komputera po zakończeniu instalacji.
      Jest bezpiecznie usunąć karta microSD bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karty microSD po zakończeniu.
   6. Włóż kartę microSD do Twojej Pi.

![Włóż kartę SD.](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Włącz Pi
Włącz Pi przy użyciu micro kabla USB i zasilania.

![Włącz](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Ważne jest, aby używać źródła zasilania w zestawie, który jest co najmniej 2A, aby upewnić się, że Twoje malina ma wystarczająco dużo mocy działała prawidłowo.

## <a name="enable-ssh"></a>Włącz SSH
Począwszy od wersji listopada 2016 Raspbian zawiera serwer SSH, domyślnie wyłączone. Musisz włączyć ją ręcznie. Można odwołać się do [oficjalnego instrukcje](https://www.raspberrypi.org/documentation/remote-access/ssh/) lub połączyć z monitorem i przejdź do **Preferencje -> Konfiguracja Pi malina** umożliwiające SSH.

## <a name="connect-raspberry-pi-3-to-the-network"></a>Połączenie z siecią 3 Pi malina
Pi można podłączyć do sieci przewodowej lub bezprzewodowej sieci. Upewnij się, że Pi jest podłączony do sieci z komputera. Na przykład można połączyć Pi do tego samego przełącznika, że komputer jest połączony.

### <a name="connect-to-a-wired-network"></a>Podłącz do sieci przewodowej
Podłącz Pi do sieci przewodowej za pomocą kabla Ethernet. Dwa LED na Pi włączyć, jeśli połączenie zostanie nawiązane.

![Połącz za pomocą kabla Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a>Połącz się z siecią bezprzewodową
Postępuj zgodnie z [instrukcje](https://www.raspberrypi.org/learning/software-guide/wifi/) z malina Foundation Pi do Pi nawiązania połączenia z siecią bezprzewodową. Te instrukcje trzeba najpierw połączyć monitora i klawiatury do Pi.

## <a name="connect-the-led-to-pi"></a>Nawiązać LED Pi
Aby wykonać to zadanie, należy użyć [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), przewodów łącznika, LED i opornik. Podłącz je do [ogólnego przeznaczenia wejścia/wyjścia](https://www.raspberrypi.org/documentation/usage/gpio/) portów (interfejs GPIO) pi.

![Breadboard LED i rezystor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Połącz krótszą etap LED do **GND interfejs GPIO (numer Pin 6)**.
2. Etap dłużej LED nawiązać połączenia z jednym etap opornik.
3. Połącz innych etap opornik do **interfejs GPIO 4 (numer Pin 7)**.

Należy pamiętać, że bieguna LED ważne. To ustawienie bieguna jest często nazywana Active niski.

![Szablon](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Gratulacje! Pomyślnie skonfigurowano Pi.

## <a name="summary"></a>Podsumowanie
W tym artykule kiedy znasz już sposobu konfigurowania Pi przez zainstalowanie Raspbian, Pi nawiązywania połączenia z siecią i nawiązywanie LED Pi. Należy pamiętać, że jeszcze nie podświetlony LED. Następne zadanie jest Zainstaluj niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia aplikacji przykładowej na Pi.

![Sprzęt jest gotowy](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

