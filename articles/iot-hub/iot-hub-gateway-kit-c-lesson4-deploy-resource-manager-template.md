---
title: "Urządzeń Sensor tag & bramy IoT Azure - lekcja 4: tworzenie aplikacji funkcji | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Intel NUC do Centrum IoT, zapisanie ich do magazynu tabel Azure, a następnie przeczytaj je z chmury."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Zapisywanie danych w chmurze, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 717c91e8332660f19d596c05a8a23afd8df1d51c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Tworzenie aplikacji funkcji i konta magazynu platformy Azure

Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie _funkcje_ (małych fragmentów kodu) w chmurze. Aplikacja Azure funkcji obsługuje wykonywanie funkcji na platformie Azure. 

## <a name="what-you-will-do"></a>Będzie wykonywać

- Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konto magazynu platformy Azure. Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure.

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak używać usługi Azure Resource Manager do wdrażania zasobów platformy Azure.
- Jak używać aplikacji Azure — funkcja przetwarzanie wiadomości Centrum IoT i zapisywania ich w tabeli w magazynie tabel platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne

Użytkownik pomyślnie ukończona poprzedniej — lekcje:

- [Lekcja 1: Konfigurowanie programu NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [Lekcja 2: Przygotowanie komputera hosta i Centrum Azure IoT](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [Lekcja 3: Odbieranie komunikatów z Sensor tag i odbieranie wiadomości z Centrum IoT](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Otwórz przykładowej aplikacji

Przejdź do Twojej `iot-hub-c-intel-nuc-gateway-getting-started` folderu repozytorium zainicjować pliki konfiguracji, a następnie otwórz przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenie:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struktura repozytorium](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- `arm-template.json` Plik jest szablonu usługi Azure Resource Manager, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.
- `arm-template-param.json` Plik jest plikiem konfiguracji używane przez szablon usługi Azure Resource Manager.
- `ReceiveDeviceMessages` Podfolder zawiera kodu Node.js dla funkcji platformy Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure

Aktualizacja `arm-template-param.json` pliku w Visual Studio Code.

![Szablon ARM w formacie json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Zastąp `[your IoT Hub name]` z `{my hub name}` określonej Lekcja 2.

Po zaktualizowaniu `arm-template-param.json` plików, wdrażanie zasobów na platformie Azure, uruchamiając następujące polecenie:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Użyj `iot-gateway` jako wartość `{resource group name}` nie zmiany wartości Lekcja 2.

## <a name="summary"></a>Podsumowanie

Po utworzeniu aplikacji Azure funkcji do przetwarzania komunikatów Centrum IoT i konto magazynu Azure do przechowywania tych wiadomości. Teraz może odczytywać wiadomości, które są wysyłane przez bramę do Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).
