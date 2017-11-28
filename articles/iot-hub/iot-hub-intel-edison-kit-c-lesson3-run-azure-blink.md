---
title: "Connect Intel Edison (C) tooAzure IoT — lekcji 3: wysyłanie komunikatów | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowych aplikacji tooIntel Edison, która wysyła Centrum IoT tooyour wiadomości i miganie hello LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania toocloud danych"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="8bc27-104">Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="8bc27-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8bc27-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="8bc27-105">What you will do</span></span>
<span data-ttu-id="8bc27-106">W tym artykule opisano sposób toodeploy i uruchom przykładową aplikację na Edison firmy Intel, który wysyła wiadomości tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8bc27-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="8bc27-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8bc27-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8bc27-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="8bc27-108">What you will learn</span></span>
<span data-ttu-id="8bc27-109">Zostanie Dowiedz się, jak toouse hello system gulp toodeploy narzędzie i uruchom hello przykładowej aplikacji C dla Edison.</span><span class="sxs-lookup"><span data-stu-id="8bc27-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8bc27-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="8bc27-110">What you need</span></span>
* <span data-ttu-id="8bc27-111">Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenie aplikacji funkcji platformy Azure i magazynu konta tooprocess i Magazyn Centrum IoT wiadomości][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="8bc27-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="8bc27-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="8bc27-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="8bc27-113">Parametry połączenia urządzenia Hello są używane tooconnect Centrum IoT tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="8bc27-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="8bc27-114">Parametry połączenia Centrum IoT Hello jest używany tooconnect tożsamości IoT hub toohello urządzenia reprezentujący Edison w Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="8bc27-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="8bc27-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="8bc27-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="8bc27-116">Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="8bc27-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="8bc27-117">Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="8bc27-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="8bc27-118">`{my hub name}`to nazwa hello określone podczas tworzenia Centrum IoT i zarejestrowana Edison.</span><span class="sxs-lookup"><span data-stu-id="8bc27-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="8bc27-119">Pobierz ciąg połączenia urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8bc27-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="8bc27-120">Użyj `myinteledison` jako wartość hello `{device id}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="8bc27-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="8bc27-121">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="8bc27-121">Configure hello device connection</span></span>
1. <span data-ttu-id="8bc27-122">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="8bc27-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="8bc27-123">Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.</span><span class="sxs-lookup"><span data-stu-id="8bc27-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="8bc27-124">Plik konfiguracji urządzenia Otwórz hello `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8bc27-124">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="8bc27-126">Wprowadź następujące elementy zastępcze w hello hello `config-edison.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="8bc27-126">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="8bc27-127">Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia hello oznaczone w dół, podczas konfigurowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8bc27-127">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="8bc27-128">Zastąp **[parametry połączenia urządzenia IoT]** z hello `device connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="8bc27-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="8bc27-129">Zastąp **[parametry połączenia Centrum IoT]** z hello `iot hub connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="8bc27-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8bc27-130">Nie ma potrzeby `azure_storage_connection_string` w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="8bc27-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="8bc27-131">Zachować, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="8bc27-131">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="8bc27-132">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8bc27-132">Deploy and run hello sample application</span></span>
<span data-ttu-id="8bc27-133">Wdrażanie i uruchamianie aplikacji przykładowej hello na Edison, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8bc27-133">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="8bc27-134">Sprawdź, czy działa hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8bc27-134">Verify that hello sample application works</span></span>
<span data-ttu-id="8bc27-135">Powinny pojawić się hello LED, który jest połączony tooEdison migający co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="8bc27-135">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="8bc27-136">Za każdym razem, gdy hello LED miga, hello przykładowej aplikacji wysyła z Centrum IoT tooyour wiadomości i sprawdza, czy tę wiadomość hello została pomyślnie wysłana tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8bc27-136">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="8bc27-137">Ponadto każdy komunikat odebrany przez Centrum IoT hello jest drukowany w oknie konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="8bc27-137">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="8bc27-138">Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu wiadomości 20.</span><span class="sxs-lookup"><span data-stu-id="8bc27-138">hello sample application terminates automatically after sending 20 messages.</span></span>

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="8bc27-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="8bc27-140">Summary</span></span>
<span data-ttu-id="8bc27-141">Została wdrożona i uruchom hello nowe migania przykładowej aplikacji na Edison Centrum IoT tooyour wiadomości urządzenia do chmury toosend.</span><span class="sxs-lookup"><span data-stu-id="8bc27-141">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="8bc27-142">Jak są one zapisywane na koncie magazynu toohello teraz monitorować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="8bc27-142">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bc27-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bc27-143">Next steps</span></span>
<span data-ttu-id="8bc27-144">[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="8bc27-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md