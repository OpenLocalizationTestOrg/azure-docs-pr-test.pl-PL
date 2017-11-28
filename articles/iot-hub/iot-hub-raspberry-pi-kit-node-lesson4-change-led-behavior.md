---
title: "Połącz Pi malina (węzeł) tooAzure IoT - 4 lekcji: modyfikowanie aplikacji | Dokumentacja firmy Microsoft"
description: "Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie."
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
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="9f8fc-104">Zmień hello włączać i wyłączać zachowanie hello LED</span><span class="sxs-lookup"><span data-stu-id="9f8fc-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9f8fc-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="9f8fc-105">What you will do</span></span>
<span data-ttu-id="9f8fc-106">Dostosowywanie hello toochange wiadomości powitania LED elementu lub wyłączyć zachowanie.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="9f8fc-107">Jeśli masz problemy z poszukiwanie rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9f8fc-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9f8fc-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="9f8fc-108">What you will learn</span></span>
<span data-ttu-id="9f8fc-109">Użyj hello toochange funkcji Node.js w dodatkowych LED elementu lub wyłączyć zachowanie.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9f8fc-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="9f8fc-110">What you need</span></span>
<span data-ttu-id="9f8fc-111">Pomyślnie zakończono [Uruchom przykładową aplikację na tooreceive Pi malina wiadomości chmury do urządzenia](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="9f8fc-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="9f8fc-112">Dodawanie funkcji Node.js</span><span class="sxs-lookup"><span data-stu-id="9f8fc-112">Add Node.js functions</span></span>
1. <span data-ttu-id="9f8fc-113">Otwórz aplikację przykładową hello kodu programu Visual Studio, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="9f8fc-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="9f8fc-114">Otwórz hello `app.js` pliku, a następnie dodaj następujące funkcje na końcu hello hello:</span><span class="sxs-lookup"><span data-stu-id="9f8fc-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![dodano funkcje pliku App.js](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="9f8fc-116">Dodaj następujące warunki przed domyślny hello w bloku przełącznika przypadku hello hello hello `receiveMessageCallback` funkcji:</span><span class="sxs-lookup"><span data-stu-id="9f8fc-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="9f8fc-117">Teraz skonfigurowaniu hello przykładowej aplikacji toorespond toomore instrukcje za pośrednictwem wiadomości.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="9f8fc-118">Witaj, "włączone" instrukcji włącza hello LED i hello "instrukcji off" wyłącza hello LED.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="9f8fc-119">Otwórz plik gulpfile.js hello, a następnie dodaj nową funkcję przed funkcją hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="9f8fc-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="9f8fc-121">W hello `sendMessage` działać, Zastąp wiersza hello `var message = buildMessage(sentMessageCount);` z nowego wiersza hello pokazano hello następującego fragmentu:</span><span class="sxs-lookup"><span data-stu-id="9f8fc-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="9f8fc-122">Zapisz wszystkie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="9f8fc-123">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="9f8fc-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="9f8fc-124">Wdrażanie i uruchamianie aplikacji przykładowej hello na Pi, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="9f8fc-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="9f8fc-125">Powinna zostać wyświetlona hello LED Włącz dla dwóch sekund, a następnie włącz poza dla innego dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="9f8fc-126">Ostatni komunikat "stop" Hello zatrzymuje hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-126">hello last "stop" message stops hello sample application from running.</span></span>

![Przykładowa aplikacja z włączać i wyłączać wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="9f8fc-128">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="9f8fc-128">Congratulations!</span></span> <span data-ttu-id="9f8fc-129">Wiadomości powitania, które są wysyłane tooPi z Centrum IoT pomyślnie zostały dostosowane.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="9f8fc-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9f8fc-130">Summary</span></span>
<span data-ttu-id="9f8fc-131">Ta sekcja opcjonalna pokazano, jak toocustomize wiadomości, dzięki czemu hello przykładowej aplikacji może kontrolować hello włączać i wyłączać zachowanie hello LED w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="9f8fc-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

