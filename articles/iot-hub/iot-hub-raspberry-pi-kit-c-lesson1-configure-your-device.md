---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie malina Pi 3 do pierwszego użycia i zainstaluj hello Raspbian systemu operacyjnego, bezpłatna systemu operacyjnego, który jest zoptymalizowana pod kątem hello Pi malina sprzętu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspbian instalacji, pobierania raspbian sposób łączenia raspbian Instalatora malinowe pi instalacji raspbian malinowe pi instalacji systemu operacyjnego, malinowe pi sd karty instalacji malinowe pi tooinstall raspbian połączyć tooraspberry pi malinowe pi łączność"
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
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Konfigurowanie urządzenia
## <a name="what-you-will-do"></a>Będzie wykonywać
Konfigurowanie Pi do pierwszego użycia i zainstaluj system operacyjny Raspbian hello. Raspbian jest bezpłatna systemu operacyjnego, który jest zoptymalizowana pod kątem hello Pi malina sprzętu. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak tooinstall Raspbian na Pi.
* Jak toopower się Pi przy użyciu kabla USB.
* Jak tooconnect Pi toohello sieci za pomocą kabla Ethernet lub sieci bezprzewodowej.
* Jak breadboard tooadd toohello LED i podłącz go tooPi.

## <a name="what-you-need"></a>Co jest potrzebne
toocomplete tej operacji, należy po części z Twojej malina Pi 3 Starter Kit hello:

* Witaj tablicy malina Pi 3
* Karta microSD 16 GB Hello
* Hello 5 volt 2-amp zasilacz za hello stopy 6 micro kabla USB
* Witaj breadboard
* Przewodów łącznika
* Ohm — 560 opornikiem
* Rozproszona LED 10 mm
* Witaj kabla Ethernet

![Elementy w zestawie początkowy](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Wymagane są również:

* Połączenie przewodowe i bezprzewodowe dla tooconnect Pi do.
* USB SD karty mini SD karty tooburn hello systemu operacyjnego obrazu lub na karcie microSD hello.
* Komputer z systemem Windows, Mac lub Linux. komputer Hello jest używany tooinstall Raspbian na karcie microSD hello.
* Toodownload połączenia internetowego hello niezbędne narzędzia i oprogramowania.

## <a name="install-raspbian-on-hello-microsd-card"></a>Zainstaluj na karcie MicroSD hello Raspbian
Przygotuj karty microSD hello instalacji hello Raspbian obrazu.

1. Pobierz Raspbian.
   1. [Pobierz](https://www.raspberrypi.org/downloads/raspbian/) pliku zip hello Joasia Raspbian z pikseli.
   2. Wyodrębnij hello Raspbian obrazu tooa folderu na komputerze.
2. Instalowanie karty microSD toohello Raspbian.
   1. [Pobierz](https://www.etcher.io) i zainstaluj narzędzie palnika karty Etcher SD hello.
   2. Uruchom Etcher i wybierz hello Raspbian obrazu, który został wyodrębniony w kroku 1.
   3. Wybierz dysk karty microSD hello.
      Należy pamiętać, że Etcher może już wybrane hello poprawnego dysku.
   4. Kliknij przycisk **Flash** karta microSD toohello Raspbian tooinstall.
   5. Karta microSD hello należy usunąć z komputera po zakończeniu instalacji.
      Jest karta microSD hello bezpieczne tooremove bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karta microSD powitania po zakończeniu.
   6. Włóż kartę microSD hello do Twojej Pi.

![Włóż kartę hello SD.](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Włącz Pi
Włącz Pi przy użyciu kabla USB micro hello i hello zasilania.

![Włącz](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Jest ważne toouse hello zasilacz w zestawie hello, który jest co najmniej 2A toomake się, że Twoje malina poprawnie ma za mało toowork zasilania.

## <a name="enable-ssh"></a>Włącz SSH
Począwszy od wersji listopada 2016 hello Raspbian ma serwer SSH hello domyślnie wyłączone. Należy tooenable go ręcznie. Może się odwoływać toohello [oficjalnego instrukcje](https://www.raspberrypi.org/documentation/remote-access/ssh/) lub połączyć z monitorem i przejść za**Preferencje -> Konfiguracja Pi malina** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Łączenie z siecią toohello malina Pi 3
Możesz połączyć tooa Pi przewodowej sieci lub tooa sieci bezprzewodowej. Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera. Na przykład możesz połączyć toohello Pi, które same przełącznika, że komputer jest podłączony do.

### <a name="connect-tooa-wired-network"></a>Łączenie ich z przewodową siecią tooa
Użyj tooconnect kabla Ethernet hello tooyour Pi ich z przewodową siecią. Witaj dwie LED Pi włączyć Jeśli hello połączenie zostanie nawiązane.

![Połącz za pomocą kabla Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Łączenie z siecią bezprzewodową tooa
Wykonaj hello [instrukcje](https://www.raspberrypi.org/learning/software-guide/wifi/) z hello Foundation Pi malina tooconnect Pi tooyour bezprzewodowej sieci. Instrukcje te wymagają toofirst połączyć z monitorem i tooPi klawiatury.

## <a name="connect-hello-led-toopi"></a>Połącz tooPi hello LED
toocomplete tego zadania, użyj hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello przewodów łącznika hello LED i hello rezystor. Podłącz je toohello [ogólnego przeznaczenia wejścia/wyjścia](https://www.raspberrypi.org/documentation/usage/gpio/) portów (interfejs GPIO) pi.

![Breadboard LED i rezystor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Połącz hello krótszą etap hello LED zbyt**GND interfejs GPIO (numer Pin 6)**.
2. Połącz hello dłużej etap hello etap tooone LED rezystor hello.
3. Połącz hello innych etap rezystor hello zbyt**interfejs GPIO 4 (numer Pin 7)**.

Należy pamiętać, że bieguna hello LED ważne. To ustawienie bieguna jest często nazywana Active niski.

![Szablon](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Gratulacje! Pomyślnie skonfigurowano Pi.

## <a name="summary"></a>Podsumowanie
W tym artykule, kiedy znasz już jak tooconfigure Pi przez zainstalowanie Raspbian, łączącego Pi tooa sieci i łączenie tooPi LED. Należy pamiętać, że powitalne LED jeszcze nie podświetlony. następne zadanie Hello jest tooinstall hello niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia aplikacji przykładowej na Pi.

![Sprzęt jest gotowy](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

