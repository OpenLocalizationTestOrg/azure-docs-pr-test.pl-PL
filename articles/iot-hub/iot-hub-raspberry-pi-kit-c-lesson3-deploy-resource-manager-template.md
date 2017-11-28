---
title: "Connect Raspberry pi (C) tooAzure IoT — lekcji 3: Wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "przechowywanie danych w chmurze hello, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 11aaad4935681d8b3d338779eec1b19d77cb11e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="f4e02-104">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="f4e02-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="f4e02-105">[Środowisko Azure Functions](../../articles/azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f4e02-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="f4e02-106">Aplikacja Azure funkcji obsługuje wykonywanie hello funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e02-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="f4e02-107">Co spowoduje zrobić</span><span class="sxs-lookup"><span data-stu-id="f4e02-107">What will you do</span></span>
<span data-ttu-id="f4e02-108">Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e02-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="f4e02-109">Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f4e02-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="f4e02-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f4e02-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="f4e02-111">Co spowoduje informacje</span><span class="sxs-lookup"><span data-stu-id="f4e02-111">What will you learn</span></span>
<span data-ttu-id="f4e02-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="f4e02-112">In this article, you will learn:</span></span>
* <span data-ttu-id="f4e02-113">Jak toouse [usługi Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure zasobów.</span><span class="sxs-lookup"><span data-stu-id="f4e02-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="f4e02-114">Jak toouse Azure funkcji tooprocess aplikacji wiadomości Centrum IoT i zapisanie ich tooa tabeli magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e02-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="f4e02-115">Czego potrzebujesz</span><span class="sxs-lookup"><span data-stu-id="f4e02-115">What do you need</span></span>
* <span data-ttu-id="f4e02-116">Pomyślnie zakończono:</span><span class="sxs-lookup"><span data-stu-id="f4e02-116">You must have successfully completed:</span></span>
- [<span data-ttu-id="f4e02-117">Rozpoczynanie pracy z Twojej malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="f4e02-117">Get started with your Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)
- [<span data-ttu-id="f4e02-118">Utworzenie Centrum Azure IoT</span><span class="sxs-lookup"><span data-stu-id="f4e02-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="f4e02-119">Otwórz hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4e02-119">Open hello sample app</span></span>
<span data-ttu-id="f4e02-120">Otwórz hello przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="f4e02-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struktura repozytorium](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* <span data-ttu-id="f4e02-122">Witaj `main.c` pliku w hello `app` podfolder jest plik źródłowy klucza hello.</span><span class="sxs-lookup"><span data-stu-id="f4e02-122">hello `main.c` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="f4e02-123">Ten plik źródłowy zawiera toosend kodu hello wiadomości 20 razy tooyour IoT hub i migania hello LED dla każdego komunikatu wysyła.</span><span class="sxs-lookup"><span data-stu-id="f4e02-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="f4e02-124">Witaj `arm-template.json` pliku jest hello Azure Resource Manager szablon, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e02-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="f4e02-125">Witaj `arm-template-param.json` plik jest plikiem konfiguracji hello używane przez hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f4e02-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="f4e02-126">Witaj `ReceiveDeviceMessages` podfolder zawiera kod Node.js hello hello funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e02-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="f4e02-127">Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f4e02-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="f4e02-128">Aktualizacja hello `arm-template-param.json` pliku w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f4e02-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametry szablonu usługi Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* <span data-ttu-id="f4e02-130">Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane malina Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f4e02-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="f4e02-131">Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma.</span><span class="sxs-lookup"><span data-stu-id="f4e02-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="f4e02-132">Prefiks Hello gwarantuje, że ta nazwa zasobu hello jest konflikt tooavoid globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="f4e02-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="f4e02-133">Nie należy używać dash lub numer początkowej w hello prefiks.</span><span class="sxs-lookup"><span data-stu-id="f4e02-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="f4e02-134">Po zaktualizowaniu hello `arm-template-param.json` plików, wdrażanie hello tooAzure zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f4e02-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="f4e02-135">Trwa około pięciu minut toocreate tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f4e02-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="f4e02-136">Podczas tworzenia zasobu hello jest w toku, można przenieść na toohello kolejnym artykule.</span><span class="sxs-lookup"><span data-stu-id="f4e02-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="f4e02-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f4e02-137">Summary</span></span>
<span data-ttu-id="f4e02-138">Po utworzeniu sieci tooprocess aplikacji funkcji Azure wiadomości Centrum IoT i toostore konta magazynu Azure, te komunikaty.</span><span class="sxs-lookup"><span data-stu-id="f4e02-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="f4e02-139">Można teraz wdrożyć i uruchomić hello próbki toosend urządzenia do chmury wiadomości na Pi.</span><span class="sxs-lookup"><span data-stu-id="f4e02-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4e02-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4e02-140">Next steps</span></span>
[<span data-ttu-id="f4e02-141">Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="f4e02-141">Run a sample application toosend device-to-cloud messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

