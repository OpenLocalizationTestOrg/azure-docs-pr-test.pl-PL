---
title: "Symulowane urządzenie & brama IoT Azure — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z IoT bramy Starter Kit, utworzenie Centrum Azure IoT i połącz Centrum IoT toohello bramy"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centrum Azure iot, bramy iot, wprowadzenie hello internet rzeczy, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Rozpoczynanie pracy z IoT bramy Starter Kit z symulowane urządzenie

> [!div class="op_single_selector"]
> * [Sensor tag](iot-hub-gateway-kit-c-get-started.md)
> * [Symulowane urządzenie](iot-hub-gateway-kit-c-sim-get-started.md)

W tym samouczku, rozpoczyna się od uczenia hello podstawowe informacje dotyczące pracy z [IoT bramy Starter Kit](https://aka.ms/gateway-kit). Będzie działać z NUC firmy Intel, z systemem Linux rzeki knie. Dowiesz się, jak połączyć tooseamleesly chmury toohello urządzeń przy użyciu Centrum IoT Azure.

***
**Zestaw nie ma jeszcze?:** kliknij [tutaj](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Lekcja 1. Konfigurowanie urządzenia NUC
![Diagram end-to-end Lesson1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

W tej lekcji w hello zestawu jako bramy usługi Azure IoT ustawiona NUC firmy Intel (dalej jednostki z przetwarzania danych), zainstaluj pakiet Azure IoT krawędzi hello na NUC i uruchom funkcję bramy hello tooverify przykładowej aplikacji.

*Szacowany czas toocomplete: 15 minut*

Przejdź do zbyt[Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lekcja 2. Tworzenie centrum IoT Hub
![Diagram end-to-end Lesson2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

W tej lekcji należy zainstalować narzędzia hello i oprogramowania na komputerze hosta. Następnie możesz utworzyć bezpłatne konto platformy Azure, udostępnić Centrum Azure IoT i utworzyć pierwszego urządzenia w Centrum IoT hello.

Lekcja 1 należy wykonać przed rozpoczęciem tej lekcji.

### <a name="get-hello-tools"></a>Pobierz narzędzia hello
Zainstaluj narzędzia hello i oprogramowania na komputerze hosta.

*Szacowany czas toocomplete: 20 minut*

Przejdź do zbyt[hello narzędzia](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Tworzenie Centrum IoT i rejestrowanie urządzenia
Tworzenie grupy zasobów, obsługi administracyjnej pierwszego Centrum Azure IoT, a następnie dodaj Centrum IoT pierwszy toohello urządzenia przy użyciu hello wiersza polecenia platformy Azure.

*Szacowany czas toocomplete: 10 minut*

Przejdź do zbyt[tworzenia Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Lekcja 3: Otrzymywać wiadomości powitania symulowane urządzenie i odbieranie wiadomości z Centrum IoT
W tej lekcji użyjesz konfiguracji hello tooautomate skrypty i wykonywanie aplikacji symulowane urządzenie w Centrum. Aplikacja symulowane urządzenie Hello generuje przykładowych danych temperatury i wysyła je z modułu Centrum IoT tooan. Witaj pakietów hello danych odebranych i wysyła je Centrum IoT tooyour za pośrednictwem hello bramy struktura dostępna w programie Azure IoT Edge modułu Centrum IoT.

![Diagram end-to-end Lekcja 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Konfigurowanie i uruchamianie symulowane urządzenie
Przygotuj hello przykładowych kodów. Następnie skonfiguruj i uruchom hello symulowane urządzenie przykładowej aplikacji.

*Szacowany czas toocomplete: 15 minut*

Przejdź do zbyt[Konfigurowanie i uruchamianie symulowane urządzenie](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT
Uruchom przykładowy kod w wiadomości powitania tooread komputera hosta z Centrum IoT.

*Szacowany czas toocomplete: 15 minut*

Przejdź do zbyt[odczytywać wiadomości z Centrum IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lekcja 4: Zapisywanie wiadomości tooAzure magazynu tabel
Utwórz aplikację Azure funkcja, która pobiera komunikaty przychodzące z Centrum IoT i zapisuje je w magazynie tabel tooAzure.

![Diagram end-to-end lekcji 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure
Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konta usługi Azure Storage.

*Szacowany czas toocomplete: 10 minut*

Przejdź do zbyt[utworzyć konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure
Monitorować wiadomości powitania bramy do chmury, ponieważ są one zapisywane tooAzure magazynu tabel.

*Szacowany czas toocomplete: 5 minut*

Przejdź za[odczytywanie wiadomości utrwalane w magazynie tabel Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli masz problemy podczas lekcje hello Szukaj rozwiązań w hello [Rozwiązywanie problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) artykułu.

## <a name="explore-more"></a>Dowiedz się więcej
Odwiedź hello [strefy developer Kit bramy IoT Intel](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn więcej.
