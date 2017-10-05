---
title: "Nawiązać Arduino (C) Azure IoT — lekcji 4: modyfikowanie aplikacji | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Formant doprowadziły z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Zmień włączenia i wyłączenia zachowanie LED
## <a name="what-you-will-do"></a>Będzie wykonywać
Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Co dowiesz się
Dodatkowe funkcje Arduino umożliwia zmianę LED włączać i wyłączać zachowanie.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono [Uruchom przykładową aplikację na tablicy Arduino do odbierania chmury do urządzenia wiadomości][receive-cloud-to-device-messages].

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>Dodawanie funkcji do main.c i gulpfile.js
1. Otwórz aplikację przykładową kodu programu Visual Studio, uruchamiając następujące polecenia:

   ```bash
   cd Lesson4
   code .
   ```
2. Otwórz `app.ino` pliku, a następnie dodaj następujące funkcje po blinkLED() funkcji:

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Plik App.Ino dodane funkcje][app-ino-file]
3. Dodaj następujące warunki przed `else if` zablokować z `receiveMessageCallback` funkcji:

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   Przykładowa aplikacja odpowiedzieć na dodatkowe instrukcje za pośrednictwem wiadomości został skonfigurowany. Instrukcje "on" powoduje włączenie LED i instrukcji "off" powoduje wyłączenie LED.
4. Otwórz plik gulpfile.js, a następnie dodaj nową funkcję przed funkcji `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Plik Gulpfile.js o funkcja dodana][gulp-file-js]
5. W `sendMessage` działać, Zastąp linię `var message = buildMessage(sentMessageCount);` z nowego wiersza wyświetlany w następujący fragment kodu:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Zapisz wszystkie zmiany.

### <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na tablicy Arduino, uruchamiając następujące polecenie:

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Powinna zostać wyświetlona LED Włącz dla dwóch sekund, a następnie wyłącz dla innego dwie sekundy. Ostatni komunikat "stop" zatrzymuje uruchomienie aplikacji przykładowej.

![włączać i wyłączać][on-and-off]

Gratulacje! Pomyślnie zostały dostosowane komunikaty, które są wysyłane do tablicy Arduino z Centrum IoT.

### <a name="summary"></a>Podsumowanie
Ta sekcja opcjonalna pokazano, jak dostosować wiadomości, dzięki czemu można kontrolować w przykładowej aplikacji w inny sposób włączenia i wyłączenia zachowanie LED.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png