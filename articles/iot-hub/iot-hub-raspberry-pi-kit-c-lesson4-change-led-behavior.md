---
title: "Nawiązać malinowe Pi (C) Azure IoT — lekcji 4: modyfikowanie aplikacji | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Formant doprowadziły malinowe pi malinowe pi doprowadziły kontroli malinowe pi kontrolę doprowadziły"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b1e441b20e161f4a03d4c2c300b21aca4fedb2a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Zmień włączenia i wyłączenia zachowanie LED
## <a name="what-you-will-do"></a>Będzie wykonywać
Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
Umożliwia zmianę LED włączać i wyłączać zachowanie dodatkowe funkcje środowiska Node.js.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono [Uruchom przykładową aplikację na Pi malina do odbierania chmury do urządzenia wiadomości](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>Dodawanie funkcji do main.c i gulpfile.js
1. Otwórz aplikację przykładową kodu programu Visual Studio, uruchamiając następujące polecenia:

   ```bash
   cd Lesson4
   code .
   ```
2. Otwórz `main.c` pliku, a następnie dodaj następujące funkcje po blinkLED() funkcji:

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![plik main.c dodane funkcje](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. Dodaj następujące warunki przed domyślny w `if` zablokować z `receiveMessageCallback` funkcji:

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
   }
   ```

   ![Plik Gulpfile.js o funkcja dodana](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. W `sendMessage` działać, Zastąp linię `var message = buildMessage(sentMessageCount);` z nowego wiersza wyświetlany w następujący fragment kodu:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Zapisz wszystkie zmiany.

### <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na Pi, uruchamiając następujące polecenie:

```bash
gulp deploy && gulp run
```

Powinna zostać wyświetlona LED Włącz dla dwóch sekund, a następnie wyłącz dla innego dwie sekundy. Ostatni komunikat "stop" zatrzymuje uruchomienie aplikacji przykładowej.

![Przykładowa aplikacja z włączać i wyłączać wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

Gratulacje! Pomyślnie zostały dostosowane komunikaty, które są wysyłane do Pi z Centrum IoT.

### <a name="summary"></a>Podsumowanie
Ta sekcja opcjonalna pokazano, jak dostosować wiadomości, dzięki czemu można kontrolować w przykładowej aplikacji w inny sposób włączenia i wyłączenia zachowanie LED.
