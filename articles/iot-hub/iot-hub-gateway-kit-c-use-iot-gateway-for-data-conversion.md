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
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Użyj bramy IoT dla transformacji danych czujnika z krawędzią IoT Azure

> [!NOTE]
> Przed rozpoczęciem tego samouczka, upewnij się, że zostały ukończone powitania po — lekcje w sekwencji:
> * [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Konfigurowanie urządzenia Intel NUC jako bramy IoT)
> * [Użyj IoT bramy tooconnect rzeczy toohello cloud - tooAzure Sensor tag Centrum IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Jeden cel bramy Iot jest tooprocess zbieranych danych przed wysłaniem toohello chmury. Usługa Azure IoT krawędzi wprowadza modułów, które mogą zostać utworzone i złożony tooform hello przetwarzania danych w przepływie pracy. Moduł odbiera komunikat, wykonuje akcję na nim i przenieść ją na dla tooprocess innych modułów.

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiedz się, jak komunikaty toocreate tooconvert modułu z hello Sensor tag do innego formatu.

## <a name="what-you-do"></a>Co zrobić

* Utwórz tooconvert modułu odebranego komunikatu do formatu JSON hello.
* Kompiluj moduł hello.
* Dodaj hello modułu toohello cz przykładowej aplikacji od Azure IoT krawędzi.
* Uruchom hello przykładowej aplikacji.

## <a name="what-you-need"></a>Co jest potrzebne

* następujące samouczki zostało ukończone w sekwencji Hello:
  * [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Konfigurowanie urządzenia Intel NUC jako bramy IoT)
  * [Użyj IoT bramy tooconnect rzeczy toohello cloud - tooAzure Sensor tag Centrum IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Klient SSH, który jest uruchamiany na komputerze hosta. PuTTY jest zalecane w systemie Windows. Linux i macOS już dostarczane za pomocą klienta SSH.
* adres IP Hello i hello nazwy użytkownika i hasła tooaccess hello bramy z powitania klienta SSH.
* Połączenie internetowe.

## <a name="create-a-module"></a>Tworzenie modułu

1. Na komputerze hosta hello Uruchom klienta SSH hello i połącz toohello IoT bramy.
1. Klonowanie pliki źródłowe hello hello modułu konwersji z katalogu macierzystego toohello GitHub hello IoT bramy, uruchamiając następujące polecenia hello:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Jest to moduł macierzysty krawędzi Azure napisana hello język programowania C. Moduł Hello konwertuje hello formatu odebranej wiadomości powitania po jednym:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Kompiluj moduł hello

Moduł hello toocompile, uruchom następujące polecenia hello:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Możesz uzyskać `libmy_module.so` plików po ukończeniu kompilacji hello. Zanotuj ścieżkę bezwzględną hello tego pliku.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Dodaj hello modułu toohello cz przykładowej aplikacji

1. Przejdź folderu przykładów toohello, uruchamiając następujące polecenie hello:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Otwórz plik konfiguracji hello, uruchamiając następujące polecenie hello:

   ```bash
   vi ble_gateway.json
   ```

1. Dodać moduł wstawiając hello następującego kodu toohello `modules` sekcji.

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

1. Zastąp `[Your libmy_module.so path]` w kodzie hello z hello ścieżka bezwzględna hello libmy_module.so "pliku.
1. Zastąp kod hello w hello `links` sekcji z jednym następującego hello:

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

1. Naciśnij klawisz `ESC`, a następnie wpisz `:wq` toosave hello pliku.

## <a name="run-hello-sample-application"></a>Uruchom hello przykładowej aplikacji

1. Włącz hello Sensor tag.
1. Ustaw zmienną środowiskową SSL_CERT_FILE hello, uruchamiając następujące polecenie hello:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Uruchom hello przykładowej aplikacji z dodanym module hello, uruchamiając następujące polecenie hello:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Następne kroki

Pomyślnie dodano Użyj hello IoT bramy tooconvert wiadomości powitania od Sensor tag do formatu JSON hello.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
