---
title: "Connect Arduino (C) tooAzure IoT — lekcji 3: Wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "przechowywanie danych w chmurze hello, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="ea6e5-104">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="ea6e5-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="ea6e5-105">[Środowisko Azure Functions](../../articles/azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="ea6e5-106">Aplikacja Azure funkcji obsługuje wykonywanie hello funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="ea6e5-107">Co spowoduje zrobić</span><span class="sxs-lookup"><span data-stu-id="ea6e5-107">What will you do</span></span>
<span data-ttu-id="ea6e5-108">Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="ea6e5-109">Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="ea6e5-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ea6e5-110">If you have any problems, look for solutions on hello [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="ea6e5-111">Co spowoduje informacje</span><span class="sxs-lookup"><span data-stu-id="ea6e5-111">What will you learn</span></span>
<span data-ttu-id="ea6e5-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="ea6e5-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ea6e5-113">Jak toouse [usługi Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="ea6e5-114">Jak toouse Azure funkcji tooprocess aplikacji wiadomości Centrum IoT i zapisanie ich tooa tabeli magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="ea6e5-115">Czego potrzebujesz</span><span class="sxs-lookup"><span data-stu-id="ea6e5-115">What do you need</span></span>
<span data-ttu-id="ea6e5-116">Pomyślnie zakończono:</span><span class="sxs-lookup"><span data-stu-id="ea6e5-116">You must have successfully completed:</span></span>
- <span data-ttu-id="ea6e5-117">[Rozpoczynanie pracy z tablicy Arduino][get-started]</span><span class="sxs-lookup"><span data-stu-id="ea6e5-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="ea6e5-118">[Utworzenie Centrum Azure IoT][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="ea6e5-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="ea6e5-119">Otwórz hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ea6e5-119">Open hello sample app</span></span>
<span data-ttu-id="ea6e5-120">Otwórz hello przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ea6e5-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struktura repozytorium][repo-structure]

* <span data-ttu-id="ea6e5-122">Witaj `app.ino` pliku w hello `app` podfolder jest plik źródłowy klucza hello.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-122">hello `app.ino` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="ea6e5-123">Ten plik źródłowy zawiera toosend kodu hello wiadomości 20 razy tooyour IoT hub i migania hello LED dla każdego komunikatu wysyła.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="ea6e5-124">Witaj `config.json` zawiera wymagane ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-124">hello `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="ea6e5-125">Witaj `arm-template.json` pliku jest hello Azure Resource Manager szablon, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="ea6e5-126">Witaj `arm-template-param.json` plik jest plikiem konfiguracji hello używane przez hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="ea6e5-127">Witaj `ReceiveDeviceMessages` podfolder zawiera kod Node.js hello hello funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="ea6e5-128">Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ea6e5-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="ea6e5-129">Aktualizacja hello `arm-template-param.json` pliku w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametry szablonu usługi Azure Resource Manager][arm-template-params]

* <span data-ttu-id="ea6e5-131">Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane tablicy Arduino][created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="ea6e5-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="ea6e5-132">Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="ea6e5-133">Prefiks Hello gwarantuje, że ta nazwa zasobu hello jest konflikt tooavoid globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="ea6e5-134">Nie należy używać dash lub numer początkowej w hello prefiks.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="ea6e5-135">Po zaktualizowaniu hello `arm-template-param.json` plików, wdrażanie hello tooAzure zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ea6e5-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="ea6e5-136">Trwa około pięciu minut toocreate tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="ea6e5-137">Podczas tworzenia zasobu hello jest w toku, można przenieść na toohello kolejnym artykule.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="ea6e5-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ea6e5-138">Summary</span></span>
<span data-ttu-id="ea6e5-139">Po utworzeniu sieci tooprocess aplikacji funkcji Azure wiadomości Centrum IoT i toostore konta magazynu Azure, te komunikaty.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="ea6e5-140">Można teraz wdrożyć i uruchomić hello próbki toosend urządzenia do chmury wiadomości na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="ea6e5-140">You can now deploy and run hello sample toosend device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea6e5-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ea6e5-141">Next steps</span></span>
<span data-ttu-id="ea6e5-142">[Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury na tablicy Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="ea6e5-142">[Run a sample application toosend device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md