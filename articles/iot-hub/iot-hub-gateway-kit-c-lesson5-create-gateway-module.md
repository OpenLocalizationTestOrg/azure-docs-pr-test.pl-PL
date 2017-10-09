---
title: "aaaCreate Twojego pierwszego modułu Azure IoT bramy | Dokumentacja firmy Microsoft"
description: "Utwórz moduł i dodaj go tooa przykładowej aplikacji toocustomize modułu zachowania."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="fc571-103">Lekcja 5: Tworzenie pierwszego modułu Azure IoT bramy</span><span class="sxs-lookup"><span data-stu-id="fc571-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="fc571-104">Chociaż Azure IoT krawędzi pozwala modułów toobuild napisany w języku Java, .NET lub Node.js, w tym samouczku przedstawiono kroki hello tworzenia modułu w C.</span><span class="sxs-lookup"><span data-stu-id="fc571-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fc571-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="fc571-105">What you will do</span></span>

- <span data-ttu-id="fc571-106">Kompilowanie i uruchamianie hello hello_world przykładową aplikację na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="fc571-107">Utwórz moduł i skompiluj go na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="fc571-108">Dodaj hello nowy moduł toohello hello_world przykładowej aplikacji, a następnie uruchom przykładowe hello na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="fc571-109">nowy moduł Hello drukowania "hello_world" wiadomości z sygnaturą czasową.</span><span class="sxs-lookup"><span data-stu-id="fc571-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fc571-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="fc571-110">What you will learn</span></span>

- <span data-ttu-id="fc571-111">Jak toocompile i uruchom przykładową aplikację na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="fc571-112">Jak toocreate modułu.</span><span class="sxs-lookup"><span data-stu-id="fc571-112">How toocreate a module.</span></span>
- <span data-ttu-id="fc571-113">Jak tooa modułu tooadd przykładową aplikację.</span><span class="sxs-lookup"><span data-stu-id="fc571-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fc571-114">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="fc571-114">What you need</span></span>

<span data-ttu-id="fc571-115">Azure IoT krawędzi, który został zainstalowany na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="fc571-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="fc571-116">Struktura folderów</span><span class="sxs-lookup"><span data-stu-id="fc571-116">Folder structure</span></span>

<span data-ttu-id="fc571-117">W podfolderze hello 5 lekcji hello przykładowy kod, który sklonowany w Lekcja 1, jest `module` folderu i `sample` folderu.</span><span class="sxs-lookup"><span data-stu-id="fc571-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="fc571-119">Witaj `module/my_module` folder zawiera hello kodu i skrypt toobuild hello modułu źródła.</span><span class="sxs-lookup"><span data-stu-id="fc571-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="fc571-120">Witaj `sample` folder zawiera hello źródła kodu i skrypt toobuild hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fc571-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="fc571-121">Kompilowanie i uruchamianie hello hello_world przykładową aplikację na Intel NUC</span><span class="sxs-lookup"><span data-stu-id="fc571-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="fc571-122">Witaj `hello_world` przykładowe tworzy bramy oparte na powitania `hello_world.json` pliku, który określa hello wstępnie zdefiniowane moduły skojarzone z aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="fc571-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="fc571-123">Dzienniki bramy Hello pliku tooa komunikat "hello world" co 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="fc571-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="fc571-124">W tej sekcji możesz skompilować i uruchomić hello `hello_world` aplikacji za pomocą jego domyślnego modułu.</span><span class="sxs-lookup"><span data-stu-id="fc571-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="fc571-125">Witaj toocompile i uruchom `hello_world` aplikacji, wykonaj następujące kroki na komputerze hosta:</span><span class="sxs-lookup"><span data-stu-id="fc571-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="fc571-126">Inicjowanie hello pliki konfiguracyjne, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="fc571-127">Aktualizuj plik konfiguracji bramy hello z hello adres MAC Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="fc571-128">Pomiń ten krok, jeśli przejściu lekcji hello zbyt[konfigurowania i uruchamiania aplikacji przykładowej cz][config_ble].</span><span class="sxs-lookup"><span data-stu-id="fc571-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="fc571-129">Otwórz plik konfiguracji bramy hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="fc571-130">Adresów MAC bramy hello aktualizacji, gdy można [Konfigurowanie NUC Intel jako brama IoT][setup_nuc], a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="fc571-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="fc571-131">Kompiluj hello przykładowy kod źródłowy, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="fc571-132">Witaj polecenia przesyła hello próbki źródła kodu tooIntel NUC i uruchamia `build.sh` toocompile go.</span><span class="sxs-lookup"><span data-stu-id="fc571-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="fc571-133">Uruchom hello `hello_world` aplikacji na NUC firmy Intel, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="fc571-134">Witaj uruchamia polecenie `../Tools/run-hello-world.js` określonym w `config.json` toostart hello przykładową aplikację na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="fc571-136">Utwórz nowy moduł i skompiluj go na Intel NUC</span><span class="sxs-lookup"><span data-stu-id="fc571-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="fc571-137">Poniższe kroki Hello przeprowadzi użytkownika przez proces tworzenia nowego modułu i skompiluj go na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="fc571-138">Moduł Hello drukowania wiadomości z sygnaturą czasową po otrzymaniu ich.</span><span class="sxs-lookup"><span data-stu-id="fc571-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="fc571-139">W tej sekcji utworzysz pierwszego modułu dostosowane bramy.</span><span class="sxs-lookup"><span data-stu-id="fc571-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="fc571-140">Każdy moduł Azure IoT krawędzi musi implementować następujące interfejsy hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="fc571-141">Opcjonalnie można zaimplementować powitania po interfejsu:</span><span class="sxs-lookup"><span data-stu-id="fc571-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="fc571-142">Witaj Poniższy diagram przedstawia hello ścieżek ważne stanu modułu.</span><span class="sxs-lookup"><span data-stu-id="fc571-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="fc571-143">prostokąty kwadratowy Hello reprezentują metody zaimplementuj tooperform operacji, gdy moduł hello są przenoszone między stanami.</span><span class="sxs-lookup"><span data-stu-id="fc571-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="fc571-144">elipsy Hello są Stany głównych, które może być moduł hello w.</span><span class="sxs-lookup"><span data-stu-id="fc571-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="fc571-146">Teraz Utwórzmy modułu na podstawie szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="fc571-147">Otwórz folder szablonu hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="fc571-149">`src/my_module.c`Służy jako szablon, który ułatwia tworzenie hello modułu.</span><span class="sxs-lookup"><span data-stu-id="fc571-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="fc571-150">Szablon Hello deklaruje hello interfejsów.</span><span class="sxs-lookup"><span data-stu-id="fc571-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="fc571-151">Toodo wystarczy toohello logiki tooadd `MyModule_Receive` funkcji.</span><span class="sxs-lookup"><span data-stu-id="fc571-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="fc571-152">`build.sh`jest moduł skryptu kompilacji hello hello toocompile na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="fc571-153">Otwórz hello `src/my_module.c` plików i zawierać dwa pliki nagłówkowe:</span><span class="sxs-lookup"><span data-stu-id="fc571-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="fc571-154">Dodaj hello następującego kodu toohello `MyModule_Receive` funkcji:</span><span class="sxs-lookup"><span data-stu-id="fc571-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="fc571-155">Aktualizacja hello `config.json` hello toospecify pliku `workspace` folderu na hosta komputera i hello ścieżka wdrożeniowa na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fc571-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="fc571-156">Podczas kompilowania, hello pliki w hello `workspace` folderu to ścieżka toohello przekazanych do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fc571-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="fc571-157">Otwórz hello `config.json` pliku, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="fc571-158">Aktualizacja `config.json` z hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fc571-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="fc571-160">Kompiluj moduł hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="fc571-161">Witaj polecenia przesyła hello źródła kodu tooIntel NUC i uruchamia `build.sh` toocompile hello modułu.</span><span class="sxs-lookup"><span data-stu-id="fc571-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="fc571-162">Dodaj hello modułu toohello hello_world przykładową aplikację i uruchamianie aplikacji hello na Intel NUC</span><span class="sxs-lookup"><span data-stu-id="fc571-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="fc571-163">tooperform to zadanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fc571-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="fc571-164">Lista wszystkich plików hello dostępne modułu binarnych (pliki .so) na Intel NUC, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="fc571-165">ścieżka binarna Hello z `my_module` można skompilować powinien być wyświetlany jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="fc571-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="fc571-166">Jeśli zmienisz nazwę użytkownika logowania domyślne hello w `config-gateway.json`, ścieżka binarna hello rozpoczyna się od `home/<your username>` zamiast `root`.</span><span class="sxs-lookup"><span data-stu-id="fc571-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="fc571-167">Dodaj `my_module` toohello `hello_world` przykładową aplikację:</span><span class="sxs-lookup"><span data-stu-id="fc571-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="fc571-168">Otwórz hello `hello_world.json` pliku, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="fc571-169">Dodaj hello następującego kodu toohello `modules` sekcji:</span><span class="sxs-lookup"><span data-stu-id="fc571-169">Add hello following code toohello `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="fc571-170">Witaj wartość `module.path` powinien być `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="fc571-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="fc571-171">Witaj kod deklaruje `my_module` toobe skojarzone z hello bramy, a także lokalizacji hello hello binarnego modułu określonego w `module.path`.</span><span class="sxs-lookup"><span data-stu-id="fc571-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="fc571-172">Dodaj hello następującego kodu toohello `links` sekcji:</span><span class="sxs-lookup"><span data-stu-id="fc571-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="fc571-173">Ten kod określa, czy komunikaty są przekazywane z hello `hello_world` modułu zbyt`my_module`.</span><span class="sxs-lookup"><span data-stu-id="fc571-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="fc571-175">Uruchom hello `hello_world` przykładowej aplikacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc571-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="fc571-176">Witaj `--config` parametru wymusza hello `run-hello-world.js` skryptu toorun przy użyciu hello `hello_world.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="fc571-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="fc571-178">Gratulacje.</span><span class="sxs-lookup"><span data-stu-id="fc571-178">Congratulations.</span></span> <span data-ttu-id="fc571-179">Możesz teraz przeglądać hello zachowanie to nowy moduł, po prostu wyświetla komunikaty "hello world" z sygnaturą czasową, innych wyników z oryginalnego modułu "hello_world" hello.</span><span class="sxs-lookup"><span data-stu-id="fc571-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc571-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc571-180">Next Steps</span></span>

<span data-ttu-id="fc571-181">Został utworzony nowy moduł, dodać przykładowe hello_world toohello i get hello przykładowej aplikacji toorun z nowego modułu hello na bramie.</span><span class="sxs-lookup"><span data-stu-id="fc571-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="fc571-182">Należy toolearn więcej o modułach bramy Azure IoT można znaleźć więcej przykładów w tym miejscu moduł: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="fc571-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
