---
title: "Pi malinowe (węzeł) nawiązania połączenia platformy Azure IoT — lekcji 4: modyfikowanie aplikacji | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant doprowadziły malinowe pi malinowe pi doprowadziły kontroli malinowe pi kontrolę doprowadziły"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b2ae23ac9cc1723936c4b4e1900b95cdcde744df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="44b7d-104">Zmień włączenia i wyłączenia zachowanie LED</span><span class="sxs-lookup"><span data-stu-id="44b7d-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="44b7d-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="44b7d-105">What you will do</span></span>
<span data-ttu-id="44b7d-106">Dostosowywanie wiadomości, aby zmienić LED włączać i wyłączać zachowanie.</span><span class="sxs-lookup"><span data-stu-id="44b7d-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="44b7d-107">Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="44b7d-107">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="44b7d-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="44b7d-108">What you will learn</span></span>
<span data-ttu-id="44b7d-109">Umożliwia zmianę LED włączać i wyłączać zachowanie dodatkowe funkcje środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="44b7d-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="44b7d-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="44b7d-110">What you need</span></span>
<span data-ttu-id="44b7d-111">Pomyślnie zakończono [Uruchom przykładową aplikację na Pi malina do odbierania wiadomości chmury do urządzenia](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="44b7d-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="44b7d-112">Dodawanie funkcji Node.js</span><span class="sxs-lookup"><span data-stu-id="44b7d-112">Add Node.js functions</span></span>
1. <span data-ttu-id="44b7d-113">Otwórz aplikację przykładową kodu programu Visual Studio, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="44b7d-113">Open the sample application in Visual Studio code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="44b7d-114">Otwórz `app.js` pliku, a następnie dodaj następujące funkcje na końcu:</span><span class="sxs-lookup"><span data-stu-id="44b7d-114">Open the `app.js` file, and then add the following functions at the end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![dodano funkcje pliku App.js](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="44b7d-116">Dodaj następujące warunki przed domyślną co w przypadku przełącznika bloku `receiveMessageCallback` funkcji:</span><span class="sxs-lookup"><span data-stu-id="44b7d-116">Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="44b7d-117">Przykładowa aplikacja odpowiedzieć na dodatkowe instrukcje za pośrednictwem wiadomości został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="44b7d-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="44b7d-118">Instrukcje "on" powoduje włączenie LED i instrukcji "off" powoduje wyłączenie LED.</span><span class="sxs-lookup"><span data-stu-id="44b7d-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="44b7d-119">Otwórz plik gulpfile.js, a następnie dodaj nową funkcję przed funkcji `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="44b7d-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>
   
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
   
   ![Plik Gulpfile.js o funkcja dodana](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. <span data-ttu-id="44b7d-121">W `sendMessage` działać, Zastąp linię `var message = buildMessage(sentMessageCount);` z nowego wiersza wyświetlany w następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="44b7d-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="44b7d-122">Zapisz wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="44b7d-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="44b7d-123">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="44b7d-123">Deploy and run the sample application</span></span>
<span data-ttu-id="44b7d-124">Wdrażanie i uruchamianie przykładowej aplikacji na Pi, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="44b7d-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="44b7d-125">Powinna zostać wyświetlona LED Włącz dla dwóch sekund, a następnie wyłącz dla innego dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="44b7d-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="44b7d-126">Ostatni komunikat "stop" zatrzymuje uruchomienie aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="44b7d-126">The last "stop" message stops the sample application from running.</span></span>

![Przykładowa aplikacja z włączać i wyłączać wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="44b7d-128">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="44b7d-128">Congratulations!</span></span> <span data-ttu-id="44b7d-129">Pomyślnie zostały dostosowane komunikaty, które są wysyłane do Pi z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44b7d-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="44b7d-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="44b7d-130">Summary</span></span>
<span data-ttu-id="44b7d-131">Ta sekcja opcjonalna pokazano, jak dostosować wiadomości, dzięki czemu można kontrolować w przykładowej aplikacji w inny sposób włączenia i wyłączenia zachowanie LED.</span><span class="sxs-lookup"><span data-stu-id="44b7d-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

