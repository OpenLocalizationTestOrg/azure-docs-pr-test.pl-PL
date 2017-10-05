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
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="059a5-104">Zmień włączenia i wyłączenia zachowanie LED</span><span class="sxs-lookup"><span data-stu-id="059a5-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="059a5-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="059a5-105">What you will do</span></span>
<span data-ttu-id="059a5-106">Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie.</span><span class="sxs-lookup"><span data-stu-id="059a5-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="059a5-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="059a5-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="059a5-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="059a5-108">What you will learn</span></span>
<span data-ttu-id="059a5-109">Dodatkowe funkcje Arduino umożliwia zmianę LED włączać i wyłączać zachowanie.</span><span class="sxs-lookup"><span data-stu-id="059a5-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="059a5-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="059a5-110">What you need</span></span>
<span data-ttu-id="059a5-111">Pomyślnie zakończono [Uruchom przykładową aplikację na tablicy Arduino do odbierania chmury do urządzenia wiadomości][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="059a5-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="059a5-112">Dodawanie funkcji do main.c i gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="059a5-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="059a5-113">Otwórz aplikację przykładową kodu programu Visual Studio, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="059a5-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="059a5-114">Otwórz `app.ino` pliku, a następnie dodaj następujące funkcje po blinkLED() funkcji:</span><span class="sxs-lookup"><span data-stu-id="059a5-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="059a5-116">Dodaj następujące warunki przed `else if` zablokować z `receiveMessageCallback` funkcji:</span><span class="sxs-lookup"><span data-stu-id="059a5-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="059a5-117">Przykładowa aplikacja odpowiedzieć na dodatkowe instrukcje za pośrednictwem wiadomości został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="059a5-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="059a5-118">Instrukcje "on" powoduje włączenie LED i instrukcji "off" powoduje wyłączenie LED.</span><span class="sxs-lookup"><span data-stu-id="059a5-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="059a5-119">Otwórz plik gulpfile.js, a następnie dodaj nową funkcję przed funkcji `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="059a5-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="059a5-121">W `sendMessage` działać, Zastąp linię `var message = buildMessage(sentMessageCount);` z nowego wiersza wyświetlany w następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="059a5-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="059a5-122">Zapisz wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="059a5-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="059a5-123">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="059a5-123">Deploy and run the sample application</span></span>
<span data-ttu-id="059a5-124">Wdrażanie i uruchamianie przykładowej aplikacji na tablicy Arduino, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="059a5-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="059a5-125">Powinna zostać wyświetlona LED Włącz dla dwóch sekund, a następnie wyłącz dla innego dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="059a5-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="059a5-126">Ostatni komunikat "stop" zatrzymuje uruchomienie aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="059a5-126">The last "stop" message stops the sample application from running.</span></span>

![włączać i wyłączać][on-and-off]

<span data-ttu-id="059a5-128">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="059a5-128">Congratulations!</span></span> <span data-ttu-id="059a5-129">Pomyślnie zostały dostosowane komunikaty, które są wysyłane do tablicy Arduino z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="059a5-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="059a5-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="059a5-130">Summary</span></span>
<span data-ttu-id="059a5-131">Ta sekcja opcjonalna pokazano, jak dostosować wiadomości, dzięki czemu można kontrolować w przykładowej aplikacji w inny sposób włączenia i wyłączenia zachowanie LED.</span><span class="sxs-lookup"><span data-stu-id="059a5-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png