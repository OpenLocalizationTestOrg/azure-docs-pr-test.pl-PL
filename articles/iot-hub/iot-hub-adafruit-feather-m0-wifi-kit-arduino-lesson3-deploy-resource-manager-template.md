---
title: "Connect Arduino (C) do Azure IoT — lekcji 3: Wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Zapisywanie danych w chmurze, dane przechowywane w chmurze, usługi w chmurze iot"
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
ms.openlocfilehash: be6105927645ae2ec56f6885c61dbcb6faf5b11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure
[Środowisko Azure Functions](../../articles/azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze. Aplikacja Azure funkcji obsługuje wykonywanie funkcji na platformie Azure.

## <a name="what-will-you-do"></a>Co spowoduje zrobić
Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konto magazynu platformy Azure. Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure.

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-will-you-learn"></a>Co spowoduje informacje
W tym artykule dowiesz się:
* Jak używać [usługi Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) wdrażania zasobów platformy Azure.
* Jak używać aplikacji Azure — funkcja przetwarzanie wiadomości Centrum IoT i zapisywania ich w tabeli w magazynie tabel platformy Azure.

## <a name="what-do-you-need"></a>Czego potrzebujesz
Pomyślnie zakończono:
- [Rozpoczynanie pracy z tablicy Arduino][get-started]
- [Utworzenie Centrum Azure IoT][create-iot-hub]

## <a name="open-the-sample-app"></a>Otwórz przykładowej aplikacji
Otwórz przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia:

```bash
cd Lesson3
code .
```

![Struktura repozytorium][repo-structure]

* `app.ino` w pliku `app` podfolder jest plik źródłowy klucza. Ten plik źródłowy zawiera kod, aby wysłać wiadomość 20 razy do Centrum IoT i blink LED dla każdej wiadomości wysyłane.
* `config.json` Zawiera wymagane ustawienia konfiguracji.
* `arm-template.json` Plik jest szablonu usługi Azure Resource Manager, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.
* `arm-template-param.json` Plik jest plikiem konfiguracji używane przez szablon usługi Azure Resource Manager.
* `ReceiveDeviceMessages` Podfolder zawiera kodu Node.js dla funkcji platformy Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure
Aktualizacja `arm-template-param.json` pliku w Visual Studio Code.

![Parametry szablonu usługi Azure Resource Manager][arm-template-params]

* Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane tablicy Arduino][created-iot-hub-and-registered-arduino-board].
* Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma. Prefiks zapewnia, że nazwa zasobu jest globalnie unikatowy, aby uniknąć konfliktu. Nie należy używać dash lub numer początkowej w prefiksie.

Po zaktualizowaniu `arm-template-param.json` plików, wdrażanie zasobów na platformie Azure, uruchamiając następujące polecenie:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Trwa około pięciu minut utworzyć tych zasobów. Podczas tworzenia zasobu jest w toku, możesz przejść do następnego artykułu.

## <a name="summary"></a>Podsumowanie
Po utworzeniu aplikacji Azure funkcji do przetwarzania komunikatów Centrum IoT i konto magazynu Azure do przechowywania tych wiadomości. Teraz można wdrożyć i uruchomić przykładowe wysyłać urządzenia do chmury na tablicy Arduino.

## <a name="next-steps"></a>Następne kroki
[Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury na tablicy Arduino][send-device-to-cloud-messages]

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md