---
title: 'Connect Arduino (C) tooAzure IoT - 4 lekcji: modyfikowanie aplikacji | Dokumentacja firmy Microsoft'
description: "Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie."
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
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Zmień hello włączać i wyłączać zachowanie hello LED
## <a name="what-you-will-do"></a>Będzie wykonywać
Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Co dowiesz się
Użyj dodatkowych hello Arduino funkcje toochange, LED elementu lub wyłączyć zachowanie.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono [Uruchom przykładową aplikację w chmurze tooreceive tablicy Arduino wiadomości toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Dodawanie funkcji toomain.c i gulpfile.js
1. Otwórz aplikację przykładową hello kodu programu Visual Studio, uruchamiając następujące polecenia hello:

   ```bash
   cd Lesson4
   code .
   ```
2. Otwórz hello `app.ino` pliku, a następnie dodaj następujące funkcje po funkcji blinkLED() hello:

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
3. Dodaj następujące warunki przed hello hello `else if` bloku hello `receiveMessageCallback` funkcji:

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

   Teraz skonfigurowaniu hello przykładowej aplikacji toorespond toomore instrukcje za pośrednictwem wiadomości. Witaj, "włączone" instrukcji włącza hello LED i hello "instrukcji off" wyłącza hello LED.
4. Otwórz plik gulpfile.js hello, a następnie dodaj nową funkcję przed funkcją hello `sendMessage`:

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
5. W hello `sendMessage` działać, Zastąp wiersza hello `var message = buildMessage(sentMessageCount);` z nowego wiersza hello pokazano hello następującego fragmentu:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Zapisz wszystkie zmiany hello.

### <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino, uruchamiając następujące polecenie hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Powinna zostać wyświetlona hello LED Włącz dla dwóch sekund, a następnie włącz poza dla innego dwie sekundy. Ostatni komunikat "stop" Hello zatrzymuje hello przykładowej aplikacji.

![włączać i wyłączać][on-and-off]

Gratulacje! Wiadomości powitania, które są wysyłane tooyour Arduino tablicy z Centrum IoT pomyślnie zostały dostosowane.

### <a name="summary"></a>Podsumowanie
Ta sekcja opcjonalna pokazano, jak toocustomize wiadomości, dzięki czemu hello przykładowej aplikacji może kontrolować hello włączać i wyłączać zachowanie hello LED w inny sposób.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png