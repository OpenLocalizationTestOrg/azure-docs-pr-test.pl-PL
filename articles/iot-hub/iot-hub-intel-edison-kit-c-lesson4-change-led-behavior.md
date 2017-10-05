---
title: "Nawiązać Intel Edison (C) Azure IoT — lekcji 4: Blink LED | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie."
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
ms.openlocfilehash: 4852b1cca4c6186ef4857b903b771f76cc20adb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="5cc78-104">Zmień włączenia i wyłączenia zachowanie LED</span><span class="sxs-lookup"><span data-stu-id="5cc78-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5cc78-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="5cc78-105">What you will do</span></span>
<span data-ttu-id="5cc78-106">Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie.</span><span class="sxs-lookup"><span data-stu-id="5cc78-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="5cc78-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5cc78-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5cc78-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="5cc78-108">What you will learn</span></span>
<span data-ttu-id="5cc78-109">Umożliwia zmianę LED włączać i wyłączać zachowanie dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="5cc78-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5cc78-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="5cc78-110">What you need</span></span>
<span data-ttu-id="5cc78-111">Pomyślnie zakończono [Uruchom przykładową aplikację na Intel Edison do odbierania chmury do urządzenia wiadomości][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="5cc78-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="5cc78-112">Dodawanie funkcji do main.c i gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="5cc78-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="5cc78-113">Otwórz aplikację przykładową kodu programu Visual Studio, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="5cc78-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="5cc78-114">Otwórz `main.c` pliku, a następnie dodaj następujące funkcje po blinkLED() funkcji:</span><span class="sxs-lookup"><span data-stu-id="5cc78-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

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

3. <span data-ttu-id="5cc78-116">Dodaj następujące warunki przed `else if` zablokować z `receiveMessageCallback` funkcji:</span><span class="sxs-lookup"><span data-stu-id="5cc78-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="5cc78-117">Przykładowa aplikacja odpowiedzieć na dodatkowe instrukcje za pośrednictwem wiadomości został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="5cc78-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="5cc78-118">Instrukcje "on" powoduje włączenie LED i instrukcji "off" powoduje wyłączenie LED.</span><span class="sxs-lookup"><span data-stu-id="5cc78-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="5cc78-119">Otwórz plik gulpfile.js, a następnie dodaj nową funkcję przed funkcji `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="5cc78-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="5cc78-121">W `sendMessage` działać, Zastąp linię `var message = buildMessage(sentMessageCount);` z nowego wiersza wyświetlany w następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="5cc78-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="5cc78-122">Zapisz wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="5cc78-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5cc78-123">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5cc78-123">Deploy and run the sample application</span></span>
<span data-ttu-id="5cc78-124">Wdrażanie i uruchamianie przykładowej aplikacji na Edison, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5cc78-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5cc78-125">Powinna zostać wyświetlona LED Włącz dla dwóch sekund, a następnie wyłącz dla innego dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="5cc78-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="5cc78-126">Ostatni komunikat "stop" zatrzymuje uruchomienie aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="5cc78-126">The last "stop" message stops the sample application from running.</span></span>

![włączać i wyłączać][on-and-off]

<span data-ttu-id="5cc78-128">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="5cc78-128">Congratulations!</span></span> <span data-ttu-id="5cc78-129">Pomyślnie zostały dostosowane komunikaty, które są wysyłane do Edison z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5cc78-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="5cc78-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5cc78-130">Summary</span></span>
<span data-ttu-id="5cc78-131">Ta sekcja opcjonalna pokazano, jak dostosować wiadomości, dzięki czemu można kontrolować w przykładowej aplikacji w inny sposób włączenia i wyłączenia zachowanie LED.</span><span class="sxs-lookup"><span data-stu-id="5cc78-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
