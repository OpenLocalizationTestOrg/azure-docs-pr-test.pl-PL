---
title: "Symulowane urządzenie & Azure IoT bramy - 4 lekcji: zapisywanie wiadomości | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Centrum IoT tooyour Intel NUC, zapisanie ich tooAzure tabeli magazynu, a następnie przeczytaj je z chmury hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "przechowywanie danych w chmurze hello, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Tworzenie aplikacji funkcji i konta magazynu platformy Azure

Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie _funkcje_ (małych fragmentów kodu) w chmurze hello. Aplikacja Azure funkcji obsługuje wykonywanie hello funkcji na platformie Azure. 

## <a name="what-you-will-do"></a>Będzie wykonywać

- Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konto magazynu platformy Azure. Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).


## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak toouse Azure Resource Manager toodeploy zasobów platformy Azure.
- Jak toouse Azure funkcji tooprocess aplikacji wiadomości Centrum IoT i zapisanie ich tooa tabeli magazynu tabel Azure.

## <a name="what-you-need"></a>Co jest potrzebne

Możesz pomyślnie ukończona — lekcje poprzedniej hello:

- [Lekcja 1: Konfigurowanie programu NUC Intel jako brama IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [Lekcja 2: Przygotowanie komputera hosta i Centrum Azure IoT](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [Lekcja 3: Otrzymywać wiadomości powitania symulowane urządzenie i odbieranie wiadomości z Centrum IoT](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>Otwórz przykładowej aplikacji

Przejdź tooyour `iot-hub-c-intel-nuc-gateway-getting-started` folderu repozytorium, pliki konfiguracji hello zainicjować i następnie otwórz hello przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenie hello:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struktura repozytorium](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Witaj `arm-template.json` pliku jest hello Azure Resource Manager szablon, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.
- Witaj `arm-template-param.json` plik jest plikiem konfiguracji hello używane przez hello szablonu usługi Azure Resource Manager.
- Witaj `ReceiveDeviceMessages` podfolder zawiera kod Node.js hello hello funkcji platformy Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure

Aktualizacja hello `arm-template-param.json` pliku w Visual Studio Code.

![Szablon ARM w formacie json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Zastąp `[your IoT Hub name]` z `{my hub name}` określonej Lekcja 2.

Po zaktualizowaniu hello `arm-template-param.json` plików, wdrażanie hello tooAzure zasobów, uruchamiając następujące polecenie hello:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Użyj `iot-gateway` jako wartość hello `{resource group name}` nie zmiany wartości hello Lekcja 2.

## <a name="summary"></a>Podsumowanie

Po utworzeniu sieci tooprocess aplikacji funkcji Azure wiadomości Centrum IoT i toostore konta magazynu Azure, te komunikaty. Teraz może odczytywać wiadomości, które są wysyłane przez Centrum IoT tooyour bramy.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).
