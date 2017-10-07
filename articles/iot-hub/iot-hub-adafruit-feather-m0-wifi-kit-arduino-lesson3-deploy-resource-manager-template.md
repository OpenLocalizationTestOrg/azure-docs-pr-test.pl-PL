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
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure
[Środowisko Azure Functions](../../articles/azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze hello. Aplikacja Azure funkcji obsługuje wykonywanie hello funkcji na platformie Azure.

## <a name="what-will-you-do"></a>Co spowoduje zrobić
Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konto magazynu platformy Azure. Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-will-you-learn"></a>Co spowoduje informacje
W tym artykule dowiesz się:
* Jak toouse [usługi Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure zasobów.
* Jak toouse Azure funkcji tooprocess aplikacji wiadomości Centrum IoT i zapisanie ich tooa tabeli magazynu tabel Azure.

## <a name="what-do-you-need"></a>Czego potrzebujesz
Pomyślnie zakończono:
- [Rozpoczynanie pracy z tablicy Arduino][get-started]
- [Utworzenie Centrum Azure IoT][create-iot-hub]

## <a name="open-hello-sample-app"></a>Otwórz hello przykładowej aplikacji
Otwórz hello przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia hello:

```bash
cd Lesson3
code .
```

![Struktura repozytorium][repo-structure]

* Witaj `app.ino` pliku w hello `app` podfolder jest plik źródłowy klucza hello. Ten plik źródłowy zawiera toosend kodu hello wiadomości 20 razy tooyour IoT hub i migania hello LED dla każdego komunikatu wysyła.
* Witaj `config.json` zawiera wymagane ustawienia konfiguracji.
* Witaj `arm-template.json` pliku jest hello Azure Resource Manager szablon, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.
* Witaj `arm-template-param.json` plik jest plikiem konfiguracji hello używane przez hello szablonu usługi Azure Resource Manager.
* Witaj `ReceiveDeviceMessages` podfolder zawiera kod Node.js hello hello funkcji platformy Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure
Aktualizacja hello `arm-template-param.json` pliku w Visual Studio Code.

![Parametry szablonu usługi Azure Resource Manager][arm-template-params]

* Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane tablicy Arduino][created-iot-hub-and-registered-arduino-board].
* Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma. Prefiks Hello gwarantuje, że ta nazwa zasobu hello jest konflikt tooavoid globalnie unikatowe. Nie należy używać dash lub numer początkowej w hello prefiks.

Po zaktualizowaniu hello `arm-template-param.json` plików, wdrażanie hello tooAzure zasobów, uruchamiając następujące polecenie hello:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Trwa około pięciu minut toocreate tych zasobów. Podczas tworzenia zasobu hello jest w toku, można przenieść na toohello kolejnym artykule.

## <a name="summary"></a>Podsumowanie
Po utworzeniu sieci tooprocess aplikacji funkcji Azure wiadomości Centrum IoT i toostore konta magazynu Azure, te komunikaty. Można teraz wdrożyć i uruchomić hello próbki toosend urządzenia do chmury wiadomości na tablicy Arduino.

## <a name="next-steps"></a>Następne kroki
[Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury na tablicy Arduino][send-device-to-cloud-messages]

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md