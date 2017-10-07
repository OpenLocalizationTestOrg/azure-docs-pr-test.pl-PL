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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="e5336-104">Zmień hello włączać i wyłączać zachowanie hello LED</span><span class="sxs-lookup"><span data-stu-id="e5336-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e5336-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="e5336-105">What you will do</span></span>
<span data-ttu-id="e5336-106">Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie.</span><span class="sxs-lookup"><span data-stu-id="e5336-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="e5336-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="e5336-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e5336-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="e5336-108">What you will learn</span></span>
<span data-ttu-id="e5336-109">Użyj dodatkowych hello Arduino funkcje toochange, LED elementu lub wyłączyć zachowanie.</span><span class="sxs-lookup"><span data-stu-id="e5336-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e5336-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e5336-110">What you need</span></span>
<span data-ttu-id="e5336-111">Pomyślnie zakończono [Uruchom przykładową aplikację w chmurze tooreceive tablicy Arduino wiadomości toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="e5336-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="e5336-112">Dodawanie funkcji toomain.c i gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="e5336-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="e5336-113">Otwórz aplikację przykładową hello kodu programu Visual Studio, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e5336-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="e5336-114">Otwórz hello `app.ino` pliku, a następnie dodaj następujące funkcje po funkcji blinkLED() hello:</span><span class="sxs-lookup"><span data-stu-id="e5336-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="e5336-116">Dodaj następujące warunki przed hello hello `else if` bloku hello `receiveMessageCallback` funkcji:</span><span class="sxs-lookup"><span data-stu-id="e5336-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="e5336-117">Teraz skonfigurowaniu hello przykładowej aplikacji toorespond toomore instrukcje za pośrednictwem wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e5336-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="e5336-118">Witaj, "włączone" instrukcji włącza hello LED i hello "instrukcji off" wyłącza hello LED.</span><span class="sxs-lookup"><span data-stu-id="e5336-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="e5336-119">Otwórz plik gulpfile.js hello, a następnie dodaj nową funkcję przed funkcją hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="e5336-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="e5336-121">W hello `sendMessage` działać, Zastąp wiersza hello `var message = buildMessage(sentMessageCount);` z nowego wiersza hello pokazano hello następującego fragmentu:</span><span class="sxs-lookup"><span data-stu-id="e5336-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="e5336-122">Zapisz wszystkie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="e5336-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="e5336-123">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e5336-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="e5336-124">Wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e5336-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="e5336-125">Powinna zostać wyświetlona hello LED Włącz dla dwóch sekund, a następnie włącz poza dla innego dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="e5336-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="e5336-126">Ostatni komunikat "stop" Hello zatrzymuje hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5336-126">hello last "stop" message stops hello sample application from running.</span></span>

![włączać i wyłączać][on-and-off]

<span data-ttu-id="e5336-128">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="e5336-128">Congratulations!</span></span> <span data-ttu-id="e5336-129">Wiadomości powitania, które są wysyłane tooyour Arduino tablicy z Centrum IoT pomyślnie zostały dostosowane.</span><span class="sxs-lookup"><span data-stu-id="e5336-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="e5336-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e5336-130">Summary</span></span>
<span data-ttu-id="e5336-131">Ta sekcja opcjonalna pokazano, jak toocustomize wiadomości, dzięki czemu hello przykładowej aplikacji może kontrolować hello włączać i wyłączać zachowanie hello LED w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="e5336-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png