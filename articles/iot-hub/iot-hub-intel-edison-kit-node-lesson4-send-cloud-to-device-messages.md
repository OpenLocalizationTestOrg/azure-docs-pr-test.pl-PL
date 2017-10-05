---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — 4 lekcji: komunikaty | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na Edison i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty do Edison z Centrum IoT miga LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant arduino doprowadziły z sieci web, kontroli arduino przeprowadzony za pośrednictwem sieci web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="85456-105">Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="85456-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="85456-106">W tym artykule wdrożono przykładową aplikację na Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="85456-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="85456-107">Przykładowa aplikacja monitoruje komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="85456-108">Można również uruchomić zadanie gulp na komputerze do wysyłania komunikatów do Edison z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="85456-109">Gdy przykładowa aplikacja odbiera komunikaty, miga LED.</span><span class="sxs-lookup"><span data-stu-id="85456-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="85456-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="85456-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="85456-111">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="85456-111">What you will do</span></span>
* <span data-ttu-id="85456-112">Połącz przykładowej aplikacji do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="85456-113">Wdrażanie i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85456-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="85456-114">Z Centrum IoT Edison miga LED wysyłać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="85456-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="85456-115">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="85456-115">What you will learn</span></span>
<span data-ttu-id="85456-116">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="85456-116">In this article, you will learn:</span></span>
* <span data-ttu-id="85456-117">Jak monitorować komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="85456-118">Sposób wysyłania komunikatów chmury do urządzenia z Centrum IoT do Edison.</span><span class="sxs-lookup"><span data-stu-id="85456-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="85456-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="85456-119">What you need</span></span>
* <span data-ttu-id="85456-120">Edison firmy Intel, skonfigurować do używania.</span><span class="sxs-lookup"><span data-stu-id="85456-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="85456-121">Aby dowiedzieć się, jak skonfigurować Edison, zobacz [Skonfiguruj urządzenie][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="85456-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="85456-122">Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="85456-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="85456-123">Aby dowiedzieć się, jak utworzyć Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="85456-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="85456-124">Połącz przykładowej aplikacji do Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="85456-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="85456-125">Upewnij się, że jesteś w folderze repozytorium `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="85456-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="85456-126">Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="85456-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="85456-127">Plik `app` podfolder jest plik źródłowy klucza, który zawiera kod umożliwiający monitorowanie komunikatów przychodzących z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="85456-128">`blinkLED` LED miga funkcji.</span><span class="sxs-lookup"><span data-stu-id="85456-128">The `blinkLED` function blinks the LED.</span></span>

   ![Struktura repozytorium w przykładowej aplikacji][repo-structure]
2. <span data-ttu-id="85456-130">Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="85456-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="85456-131">Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje są dziedziczone, można pominąć krok do zadania, wdrażanie i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85456-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="85456-132">Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy zastąpić symbole zastępcze w `config-edison.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="85456-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="85456-133">`config-edison.json` Plik znajduje się w podfolderze folderu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="85456-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Zawartość pliku konfiguracji edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="85456-135">Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia, które są oznaczone w dół, podczas konfigurowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="85456-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="85456-136">Zastąp **[parametry połączenia urządzenia IoT]** z parametrami połączenia urządzenia, który można uzyskać, uruchamiając `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="85456-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="85456-137">Zastąp **[parametry połączenia Centrum IoT]** z parametrami połączenia Centrum IoT, który można uzyskać, uruchamiając `az iot hub show-connection-string --name {my hub name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="85456-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="85456-138">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="85456-138">Deploy and run the sample application</span></span>
<span data-ttu-id="85456-139">Wdrażanie i uruchamianie przykładowej aplikacji na Edison, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="85456-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="85456-140">Polecenie gulp wdraża przykładowej aplikacji do Edison.</span><span class="sxs-lookup"><span data-stu-id="85456-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="85456-141">Następnie uruchomi aplikację na Edison i oddzielnych zadań na komputerze hosta do wysyłania wiadomości migania 20 do Edison z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="85456-142">Po uruchomieniu aplikacji przykładowej, rozpoczyna nasłuchiwanie wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="85456-143">W tym samym czasie zadań gulp wysyła komunikaty "blink" z Centrum IoT do Edison.</span><span class="sxs-lookup"><span data-stu-id="85456-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="85456-144">Dla każdego komunikatu migania odbierająca Edison wywołuje przykładowej aplikacji `blinkLED` funkcja miga LED.</span><span class="sxs-lookup"><span data-stu-id="85456-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="85456-145">Zadanie gulp wyśle 20 komunikatów z Centrum IoT do Edison powinna zostać wyświetlona migania LED co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="85456-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="85456-146">Komunikat "stop", która kończy działanie aplikacji jest ostatni z nich.</span><span class="sxs-lookup"><span data-stu-id="85456-146">The last one is a "stop" message that stops the application from running.</span></span>

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="85456-148">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="85456-148">Summary</span></span>
<span data-ttu-id="85456-149">Na Edison miga LED zostało pomyślnie wysłane wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="85456-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="85456-150">Następne zadanie jest opcjonalne: Zmień włączenia i wyłączenia zachowanie LED.</span><span class="sxs-lookup"><span data-stu-id="85456-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85456-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85456-151">Next steps</span></span>
<span data-ttu-id="85456-152">[Zmień włączenia i wyłączenia zachowanie LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="85456-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md