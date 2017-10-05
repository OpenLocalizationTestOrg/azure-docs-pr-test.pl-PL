---
title: "Nawiązać Pi malina (węzeł) Azure IoT — lekcji 3: Wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Zapisywanie danych w chmurze, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure
[Środowisko Azure Functions](../azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze. Aplikacja Azure funkcji obsługuje wykonywanie funkcji na platformie Azure.

## <a name="what-you-will-do"></a>Będzie wykonywać
Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konto magazynu platformy Azure. Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure. Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak używać [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania zasobów platformy Azure.
* Jak używać aplikacji Azure — funkcja przetwarzanie wiadomości Centrum IoT i zapisywania ich w tabeli w magazynie tabel platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne
Pomyślnie zakończono:
* [Rozpoczynanie pracy z malina Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)
* [Utworzenie Centrum Azure IoT](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a>Otwórz przykładowej aplikacji
Otwórz przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia:

```bash
cd Lesson3
code .
```

![Struktura repozytorium](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* `app.js` w pliku `app` podfolder jest plik źródłowy klucza. Ten plik źródłowy zawiera kod, aby wysłać wiadomość 20 razy do Centrum IoT i blink LED dla każdej wiadomości wysyłane.
* `arm-template.json` Plik jest szablonu usługi Azure Resource Manager, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.
* `arm-template-param.json` Plik jest plikiem konfiguracji używane przez szablon usługi Azure Resource Manager.
* `ReceiveDeviceMessages` Podfolder zawiera kodu Node.js dla funkcji platformy Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure
Aktualizacja `arm-template-param.json` pliku w Visual Studio Code.

![Parametry szablonu usługi Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma. Prefiks zapewnia, że nazwa zasobu jest globalnie unikatowy, aby uniknąć konfliktu. Nie należy używać dash lub numer początkowej w prefiksie.

Po zaktualizowaniu `arm-template-param.json` plików, wdrażanie zasobów na platformie Azure, uruchamiając następujące polecenie:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Trwa około pięciu minut utworzyć tych zasobów. Podczas tworzenia zasobu jest w toku, możesz przejść do następnego artykułu.

## <a name="summary"></a>Podsumowanie
Po utworzeniu aplikacji Azure funkcji do przetwarzania komunikatów Centrum IoT i konto magazynu Azure do przechowywania tych wiadomości. Można teraz wdrożyć i uruchomić przykładowe wysyłać urządzenia do chmury na Pi.

## <a name="next-steps"></a>Następne kroki
[Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury w malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

