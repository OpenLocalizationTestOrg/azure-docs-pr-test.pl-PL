---
title: 'Connect Intel Edison (C) tooAzure IoT - 4 lekcji: komunikaty | Dokumentacja firmy Microsoft'
description: "Przykładowa aplikacja działa na Edison i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty tooEdison z Twojej hello tooblink Centrum IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant arduino doprowadziły z sieci web, kontroli arduino przeprowadzony za pośrednictwem sieci web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="55e8d-105">Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="55e8d-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="55e8d-106">W tym artykule wdrożono przykładową aplikację na Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="55e8d-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="55e8d-107">aplikacja przykładowa Hello monitoruje komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="55e8d-108">Można również uruchomić zadanie gulp na tooEdison wiadomości toosend Twojego komputera z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="55e8d-109">Gdy hello Przykładowa aplikacja odbiera wiadomości powitania, miga hello LED.</span><span class="sxs-lookup"><span data-stu-id="55e8d-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="55e8d-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="55e8d-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="55e8d-111">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="55e8d-111">What you will do</span></span>
* <span data-ttu-id="55e8d-112">Połącz Centrum IoT tooyour hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55e8d-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="55e8d-113">Wdrażanie i uruchamianie hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55e8d-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="55e8d-114">Wysyłanie wiadomości z Twojej IoT hub tooEdison tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="55e8d-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="55e8d-115">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="55e8d-115">What you will learn</span></span>
<span data-ttu-id="55e8d-116">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="55e8d-116">In this article, you will learn:</span></span>
* <span data-ttu-id="55e8d-117">Jak komunikaty przychodzące toomonitor z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="55e8d-118">Jak chmury urządzenia toosend komunikaty z sieci tooEdison Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55e8d-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="55e8d-119">What you need</span></span>
* <span data-ttu-id="55e8d-120">Edison firmy Intel, skonfigurować do używania.</span><span class="sxs-lookup"><span data-stu-id="55e8d-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="55e8d-121">toolearn tooset się Edison, zobacz temat [Skonfiguruj urządzenie][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="55e8d-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="55e8d-122">Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="55e8d-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="55e8d-123">toolearn jak toocreate Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="55e8d-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="55e8d-124">Połącz z Centrum IoT tooyour hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="55e8d-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="55e8d-125">Upewnij się, że jesteś w folderze repozytorium hello `iot-hub-c-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="55e8d-125">Make sure that you're in hello repo folder `iot-hub-c-edison-getting-started`.</span></span> <span data-ttu-id="55e8d-126">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="55e8d-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="55e8d-127">Plik Hello w hello `app` podfolder jest plik źródłowy klucza hello, który zawiera komunikaty przychodzące toomonitor kodu hello z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="55e8d-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="55e8d-128">Witaj `blinkLED` funkcja miganie hello LED.</span><span class="sxs-lookup"><span data-stu-id="55e8d-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Struktura repozytorium w hello przykładowej aplikacji][repo-structure]
2. <span data-ttu-id="55e8d-130">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="55e8d-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="55e8d-131">Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje hello są dziedziczone, można pominąć hello krok toohello zadania wdrażania i uruchomiona hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55e8d-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="55e8d-132">Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy symbole zastępcze hello tooreplace w hello `config-edison.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="55e8d-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="55e8d-133">Witaj `config-edison.json` plik znajduje się w podfolderze hello folderu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="55e8d-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Zawartość pliku config edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="55e8d-135">Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia hello oznaczone w dół, podczas konfigurowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="55e8d-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="55e8d-136">Zastąp **[parametry połączenia urządzenia IoT]** z hello parametry połączenia urządzenia, które można uzyskać, uruchamiając hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="55e8d-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="55e8d-137">Zastąp **[parametry połączenia Centrum IoT]** z hello parametry połączenia Centrum IoT, które można uzyskać, uruchamiając hello `az iot hub show-connection-string --name {my hub name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="55e8d-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="55e8d-138">Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.</span><span class="sxs-lookup"><span data-stu-id="55e8d-138">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="55e8d-139">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="55e8d-139">Deploy and run hello sample application</span></span>
<span data-ttu-id="55e8d-140">Wdrażanie i uruchamianie aplikacji przykładowej hello na Edison, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="55e8d-140">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="55e8d-141">polecenie gulp Hello wdraża hello przykładowej aplikacji tooEdison.</span><span class="sxs-lookup"><span data-stu-id="55e8d-141">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="55e8d-142">Następnie uruchomieniu aplikacji hello na Edison i oddzielnych zadań na hoście tooEdison wiadomości migania toosend 20 komputera z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-142">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="55e8d-143">Po uruchomieniu aplikacji przykładowej hello rozpoczyna nasłuchiwanie toomessages z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-143">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="55e8d-144">W tym samym czasie hello gulp zadań wysyła komunikaty "blink" z Twojej tooEdison Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-144">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="55e8d-145">Dla każdego komunikatu migania odbierająca Edison hello przykładowej aplikacji wywołuje hello `blinkLED` funkcja tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="55e8d-145">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="55e8d-146">Powinny pojawić się migania LED hello co dwie sekundy jako hello system gulp zadań wysyła 20 komunikatów z Twojej tooEdison Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="55e8d-146">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="55e8d-147">Hello ostatnio jedna jest zatrzymuje aplikacji hello komunikat "stop".</span><span class="sxs-lookup"><span data-stu-id="55e8d-147">hello last one is a "stop" message that stops hello application from running.</span></span>

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="55e8d-149">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="55e8d-149">Summary</span></span>
<span data-ttu-id="55e8d-150">Zostało pomyślnie wysłane wiadomości z Twojej IoT hub tooEdison tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="55e8d-150">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="55e8d-151">następne zadanie Hello jest opcjonalny: Zmień hello włączać i wyłączać zachowanie hello LED.</span><span class="sxs-lookup"><span data-stu-id="55e8d-151">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55e8d-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55e8d-152">Next steps</span></span>
<span data-ttu-id="55e8d-153">[Zmień hello włączać i wyłączać zachowanie hello LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="55e8d-153">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md