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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Lekcja 5: Tworzenie pierwszego modułu Azure IoT bramy
Chociaż Azure IoT krawędzi pozwala modułów toobuild napisany w języku Java, .NET lub Node.js, w tym samouczku przedstawiono kroki hello tworzenia modułu w C.

## <a name="what-you-will-do"></a>Będzie wykonywać

- Kompilowanie i uruchamianie hello hello_world przykładową aplikację na Intel NUC.
- Utwórz moduł i skompiluj go na Intel NUC.
- Dodaj hello nowy moduł toohello hello_world przykładowej aplikacji, a następnie uruchom przykładowe hello na Intel NUC. nowy moduł Hello drukowania "hello_world" wiadomości z sygnaturą czasową.

## <a name="what-you-will-learn"></a>Co dowiesz się

- Jak toocompile i uruchom przykładową aplikację na Intel NUC.
- Jak toocreate modułu.
- Jak tooa modułu tooadd przykładową aplikację.

## <a name="what-you-need"></a>Co jest potrzebne

Azure IoT krawędzi, który został zainstalowany na komputerze hosta.

## <a name="folder-structure"></a>Struktura folderów

W podfolderze hello 5 lekcji hello przykładowy kod, który sklonowany w Lekcja 1, jest `module` folderu i `sample` folderu.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Witaj `module/my_module` folder zawiera hello kodu i skrypt toobuild hello modułu źródła.
- Witaj `sample` folder zawiera hello źródła kodu i skrypt toobuild hello przykładowej aplikacji.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Kompilowanie i uruchamianie hello hello_world przykładową aplikację na Intel NUC

Witaj `hello_world` przykładowe tworzy bramy oparte na powitania `hello_world.json` pliku, który określa hello wstępnie zdefiniowane moduły skojarzone z aplikacją hello. Dzienniki bramy Hello pliku tooa komunikat "hello world" co 5 sekund. W tej sekcji możesz skompilować i uruchomić hello `hello_world` aplikacji za pomocą jego domyślnego modułu.

Witaj toocompile i uruchom `hello_world` aplikacji, wykonaj następujące kroki na komputerze hosta:

1. Inicjowanie hello pliki konfiguracyjne, uruchamiając następujące polecenia hello:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Aktualizuj plik konfiguracji bramy hello z hello adres MAC Intel NUC. Pomiń ten krok, jeśli przejściu lekcji hello zbyt[konfigurowania i uruchamiania aplikacji przykładowej cz][config_ble].

   1. Otwórz plik konfiguracji bramy hello, uruchamiając następujące polecenie hello:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Adresów MAC bramy hello aktualizacji, gdy można [Konfigurowanie NUC Intel jako brama IoT][setup_nuc], a następnie zapisz plik hello.

1. Kompiluj hello przykładowy kod źródłowy, uruchamiając następujące polecenie hello:

   ```bash
   gulp compile
   ```

   Witaj polecenia przesyła hello próbki źródła kodu tooIntel NUC i uruchamia `build.sh` toocompile go.

1. Uruchom hello `hello_world` aplikacji na NUC firmy Intel, uruchamiając następujące polecenie hello:

   ```bash
   gulp run
   ```

   Witaj uruchamia polecenie `../Tools/run-hello-world.js` określonym w `config.json` toostart hello przykładową aplikację na Intel NUC.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Utwórz nowy moduł i skompiluj go na Intel NUC

Poniższe kroki Hello przeprowadzi użytkownika przez proces tworzenia nowego modułu i skompiluj go na Intel NUC. Moduł Hello drukowania wiadomości z sygnaturą czasową po otrzymaniu ich. W tej sekcji utworzysz pierwszego modułu dostosowane bramy.

Każdy moduł Azure IoT krawędzi musi implementować następujące interfejsy hello:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

Opcjonalnie można zaimplementować powitania po interfejsu:

   ```C
   pfModule_Start Module_Start
   ```

Witaj Poniższy diagram przedstawia hello ścieżek ważne stanu modułu. prostokąty kwadratowy Hello reprezentują metody zaimplementuj tooperform operacji, gdy moduł hello są przenoszone między stanami. elipsy Hello są Stany głównych, które może być moduł hello w.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Teraz Utwórzmy modułu na podstawie szablonu hello:

1. Otwórz folder szablonu hello, uruchamiając następujące polecenie hello:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`Służy jako szablon, który ułatwia tworzenie hello modułu. Szablon Hello deklaruje hello interfejsów. Toodo wystarczy toohello logiki tooadd `MyModule_Receive` funkcji.
   - `build.sh`jest moduł skryptu kompilacji hello hello toocompile na Intel NUC.
1. Otwórz hello `src/my_module.c` plików i zawierać dwa pliki nagłówkowe:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Dodaj hello następującego kodu toohello `MyModule_Receive` funkcji:

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

1. Aktualizacja hello `config.json` hello toospecify pliku `workspace` folderu na hosta komputera i hello ścieżka wdrożeniowa na Intel NUC. Podczas kompilowania, hello pliki w hello `workspace` folderu to ścieżka toohello przekazanych do wdrożenia.

   1. Otwórz hello `config.json` pliku, uruchamiając następujące polecenie hello:

      ```bash
      code config.json
      ```

   1. Aktualizacja `config.json` z hello następującej konfiguracji:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Kompiluj moduł hello, uruchamiając następujące polecenie hello:

   ```bash
   gulp compile
   ```

   Witaj polecenia przesyła hello źródła kodu tooIntel NUC i uruchamia `build.sh` toocompile hello modułu.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Dodaj hello modułu toohello hello_world przykładową aplikację i uruchamianie aplikacji hello na Intel NUC

tooperform to zadanie, wykonaj następujące kroki:

1. Lista wszystkich plików hello dostępne modułu binarnych (pliki .so) na Intel NUC, uruchamiając następujące polecenie hello:

   ```bash
   gulp modules --list
   ```

   ścieżka binarna Hello z `my_module` można skompilować powinien być wyświetlany jak poniżej:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Jeśli zmienisz nazwę użytkownika logowania domyślne hello w `config-gateway.json`, ścieżka binarna hello rozpoczyna się od `home/<your username>` zamiast `root`.

1. Dodaj `my_module` toohello `hello_world` przykładową aplikację:

   1. Otwórz hello `hello_world.json` pliku, uruchamiając następujące polecenie hello:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Dodaj hello następującego kodu toohello `modules` sekcji:

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

      Witaj wartość `module.path` powinien być `/root/gateway_sample/module/my_module/build/libmy_module.so`. Witaj kod deklaruje `my_module` toobe skojarzone z hello bramy, a także lokalizacji hello hello binarnego modułu określonego w `module.path`.
   1. Dodaj hello następującego kodu toohello `links` sekcji:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Ten kod określa, czy komunikaty są przekazywane z hello `hello_world` modułu zbyt`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Uruchom hello `hello_world` przykładowej aplikacji, uruchamiając następujące polecenie hello:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Witaj `--config` parametru wymusza hello `run-hello-world.js` skryptu toorun przy użyciu hello `hello_world.json` pliku.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Gratulacje. Możesz teraz przeglądać hello zachowanie to nowy moduł, po prostu wyświetla komunikaty "hello world" z sygnaturą czasową, innych wyników z oryginalnego modułu "hello_world" hello.

## <a name="next-steps"></a>Następne kroki

Został utworzony nowy moduł, dodać przykładowe hello_world toohello i get hello przykładowej aplikacji toorun z nowego modułu hello na bramie. Należy toolearn więcej o modułach bramy Azure IoT można znaleźć więcej przykładów w tym miejscu moduł: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
