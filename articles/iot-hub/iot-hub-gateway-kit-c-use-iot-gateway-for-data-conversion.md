---
title: "Konwersja aaaData w bramie IoT Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Użyj IoT bramy tooconvert hello formatu danych czujników za pomocą dostosowanego modułu na podstawie Azure IoT krawędzi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Konwersja danych bramy iot, przekształcania danych bramy iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="e0bfe-104">Użyj bramy IoT dla transformacji danych czujnika z krawędzią IoT Azure</span><span class="sxs-lookup"><span data-stu-id="e0bfe-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="e0bfe-105">Przed rozpoczęciem tego samouczka, upewnij się, że zostały ukończone powitania po — lekcje w sekwencji:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * <span data-ttu-id="e0bfe-106">[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Konfigurowanie urządzenia Intel NUC jako bramy IoT)</span><span class="sxs-lookup"><span data-stu-id="e0bfe-106">[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>
> * [<span data-ttu-id="e0bfe-107">Użyj IoT bramy tooconnect rzeczy toohello cloud - tooAzure Sensor tag Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e0bfe-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="e0bfe-108">Jeden cel bramy Iot jest tooprocess zbieranych danych przed wysłaniem toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="e0bfe-109">Usługa Azure IoT krawędzi wprowadza modułów, które mogą zostać utworzone i złożony tooform hello przetwarzania danych w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="e0bfe-110">Moduł odbiera komunikat, wykonuje akcję na nim i przenieść ją na dla tooprocess innych modułów.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="e0bfe-111">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="e0bfe-111">What you learn</span></span>

<span data-ttu-id="e0bfe-112">Dowiedz się, jak komunikaty toocreate tooconvert modułu z hello Sensor tag do innego formatu.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="e0bfe-113">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="e0bfe-113">What you do</span></span>

* <span data-ttu-id="e0bfe-114">Utwórz tooconvert modułu odebranego komunikatu do formatu JSON hello.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="e0bfe-115">Kompiluj moduł hello.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-115">Compile hello module.</span></span>
* <span data-ttu-id="e0bfe-116">Dodaj hello modułu toohello cz przykładowej aplikacji od Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="e0bfe-117">Uruchom hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e0bfe-118">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e0bfe-118">What you need</span></span>

* <span data-ttu-id="e0bfe-119">następujące samouczki zostało ukończone w sekwencji Hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-119">hello following tutorials completed in sequence:</span></span>
  * <span data-ttu-id="e0bfe-120">[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Konfigurowanie urządzenia Intel NUC jako bramy IoT)</span><span class="sxs-lookup"><span data-stu-id="e0bfe-120">[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>
  * [<span data-ttu-id="e0bfe-121">Użyj IoT bramy tooconnect rzeczy toohello cloud - tooAzure Sensor tag Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e0bfe-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="e0bfe-122">Klient SSH, który jest uruchamiany na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="e0bfe-123">PuTTY jest zalecane w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="e0bfe-124">Linux i macOS już dostarczane za pomocą klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="e0bfe-125">adres IP Hello i hello nazwy użytkownika i hasła tooaccess hello bramy z powitania klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="e0bfe-126">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="e0bfe-127">Tworzenie modułu</span><span class="sxs-lookup"><span data-stu-id="e0bfe-127">Create a module</span></span>

1. <span data-ttu-id="e0bfe-128">Na komputerze hosta hello Uruchom klienta SSH hello i połącz toohello IoT bramy.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="e0bfe-129">Klonowanie pliki źródłowe hello hello modułu konwersji z katalogu macierzystego toohello GitHub hello IoT bramy, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="e0bfe-130">Jest to moduł macierzysty krawędzi Azure napisana hello język programowania C.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="e0bfe-131">Moduł Hello konwertuje hello formatu odebranej wiadomości powitania po jednym:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="e0bfe-132">Kompiluj moduł hello</span><span class="sxs-lookup"><span data-stu-id="e0bfe-132">Compile hello module</span></span>

<span data-ttu-id="e0bfe-133">Moduł hello toocompile, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="e0bfe-134">Możesz uzyskać `libmy_module.so` plików po ukończeniu kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="e0bfe-135">Zanotuj ścieżkę bezwzględną hello tego pliku.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="e0bfe-136">Dodaj hello modułu toohello cz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e0bfe-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="e0bfe-137">Przejdź folderu przykładów toohello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="e0bfe-138">Otwórz plik konfiguracji hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="e0bfe-139">Dodać moduł wstawiając hello następującego kodu toohello `modules` sekcji.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="e0bfe-140">Zastąp `[Your libmy_module.so path]` w kodzie hello z hello ścieżka bezwzględna hello libmy_module.so "pliku.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="e0bfe-141">Zastąp kod hello w hello `links` sekcji z jednym następującego hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="e0bfe-142">Naciśnij klawisz `ESC`, a następnie wpisz `:wq` toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="e0bfe-143">Uruchom hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e0bfe-143">Run hello sample application</span></span>

1. <span data-ttu-id="e0bfe-144">Włącz hello Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="e0bfe-145">Ustaw zmienną środowiskową SSL_CERT_FILE hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="e0bfe-146">Uruchom hello przykładowej aplikacji z dodanym module hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e0bfe-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="e0bfe-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0bfe-147">Next steps</span></span>

<span data-ttu-id="e0bfe-148">Pomyślnie dodano Użyj hello IoT bramy tooconvert wiadomości powitania od Sensor tag do formatu JSON hello.</span><span class="sxs-lookup"><span data-stu-id="e0bfe-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
