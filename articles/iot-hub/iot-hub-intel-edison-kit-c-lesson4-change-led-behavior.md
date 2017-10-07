---
title: 'Connect Intel Edison (C) tooAzure IoT - 4 lekcji: Blink hello LED | Dokumentacja firmy Microsoft'
description: "Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Formant doprowadziły z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Zmień hello włączać i wyłączać zachowanie hello LED
## <a name="what-you-will-do"></a>Będzie wykonywać
Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
Użyj LED elementu lub wyłączyć zachowanie hello toochange dodatkowe funkcje.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono [Uruchom przykładową aplikację w chmurze tooreceive Intel Edison wiadomości toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Dodawanie funkcji toomain.c i gulpfile.js
1. Otwórz aplikację przykładową hello kodu programu Visual Studio, uruchamiając następujące polecenia hello:

   ```bash
   cd Lesson4
   code .
   ```
2. Otwórz hello `main.c` pliku, a następnie dodaj następujące funkcje po funkcji blinkLED() hello:

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![plik main.c dodane funkcje](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Dodaj następujące warunki przed hello hello `else if` bloku hello `receiveMessageCallback` funkcji:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
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
   }
   ```

   ![Plik Gulpfile.js o funkcja dodana][gulpfile]
5. W hello `sendMessage` działać, Zastąp wiersza hello `var message = buildMessage(sentMessageCount);` z nowego wiersza hello pokazano hello następującego fragmentu:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Zapisz wszystkie zmiany hello.

### <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na Edison, uruchamiając następujące polecenie hello:

```bash
gulp deploy && gulp run
```

Powinna zostać wyświetlona hello LED Włącz dla dwóch sekund, a następnie włącz poza dla innego dwie sekundy. Ostatni komunikat "stop" Hello zatrzymuje hello przykładowej aplikacji.

![włączać i wyłączać][on-and-off]

Gratulacje! Wiadomości powitania, które są wysyłane tooEdison z Centrum IoT pomyślnie zostały dostosowane.

### <a name="summary"></a>Podsumowanie
Ta sekcja opcjonalna pokazano, jak toocustomize wiadomości, dzięki czemu hello przykładowej aplikacji może kontrolować hello włączać i wyłączać zachowanie hello LED w inny sposób.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
