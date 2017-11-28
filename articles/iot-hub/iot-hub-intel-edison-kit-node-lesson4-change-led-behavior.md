---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT - 4 lekcji: Blink hello LED | Dokumentacja firmy Microsoft"
description: "Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Formant doprowadziły z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="04b0b-104">Zmień hello włączać i wyłączać zachowanie hello LED</span><span class="sxs-lookup"><span data-stu-id="04b0b-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="04b0b-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="04b0b-105">What you will do</span></span>
<span data-ttu-id="04b0b-106">Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie.</span><span class="sxs-lookup"><span data-stu-id="04b0b-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="04b0b-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="04b0b-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="04b0b-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="04b0b-108">What you will learn</span></span>
<span data-ttu-id="04b0b-109">Użyj LED elementu lub wyłączyć zachowanie hello toochange dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="04b0b-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="04b0b-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="04b0b-110">What you need</span></span>
<span data-ttu-id="04b0b-111">Pomyślnie zakończono [Uruchom przykładową aplikację w chmurze tooreceive Intel Edison wiadomości toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="04b0b-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="04b0b-112">Dodawanie funkcji tooapp.js i gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="04b0b-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="04b0b-113">Otwórz aplikację przykładową hello kodu programu Visual Studio, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="04b0b-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="04b0b-114">Otwórz hello `app.js` pliku, a następnie dodaj następujące funkcje po funkcji blinkLED() hello:</span><span class="sxs-lookup"><span data-stu-id="04b0b-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![dodano funkcje pliku App.js](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="04b0b-116">Dodaj hello następujące warunki przed hello "blink" case w bloku przełącznika przypadku hello hello `receiveMessageCallback` funkcji:</span><span class="sxs-lookup"><span data-stu-id="04b0b-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="04b0b-117">Teraz skonfigurowaniu hello przykładowej aplikacji toorespond toomore instrukcje za pośrednictwem wiadomości.</span><span class="sxs-lookup"><span data-stu-id="04b0b-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="04b0b-118">Witaj, "włączone" instrukcji włącza hello LED i hello "instrukcji off" wyłącza hello LED.</span><span class="sxs-lookup"><span data-stu-id="04b0b-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="04b0b-119">Otwórz plik gulpfile.js hello, a następnie dodaj nową funkcję przed funkcją hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="04b0b-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="04b0b-121">W hello `sendMessage` działać, Zastąp wiersza hello `var message = buildMessage(sentMessageCount);` z nowego wiersza hello pokazano hello następującego fragmentu:</span><span class="sxs-lookup"><span data-stu-id="04b0b-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="04b0b-122">Zapisz wszystkie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="04b0b-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="04b0b-123">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="04b0b-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="04b0b-124">Wdrażanie i uruchamianie aplikacji przykładowej hello na Edison, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="04b0b-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="04b0b-125">Powinna zostać wyświetlona hello LED Włącz dla dwóch sekund, a następnie włącz poza dla innego dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="04b0b-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="04b0b-126">Ostatni komunikat "stop" Hello zatrzymuje hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04b0b-126">hello last "stop" message stops hello sample application from running.</span></span>

![włączać i wyłączać][on-and-off]

<span data-ttu-id="04b0b-128">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="04b0b-128">Congratulations!</span></span> <span data-ttu-id="04b0b-129">Wiadomości powitania, które są wysyłane tooEdison z Centrum IoT pomyślnie zostały dostosowane.</span><span class="sxs-lookup"><span data-stu-id="04b0b-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="04b0b-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="04b0b-130">Summary</span></span>
<span data-ttu-id="04b0b-131">Ta sekcja opcjonalna pokazano, jak toocustomize wiadomości, dzięki czemu hello przykładowej aplikacji może kontrolować hello włączać i wyłączać zachowanie hello LED w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="04b0b-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
