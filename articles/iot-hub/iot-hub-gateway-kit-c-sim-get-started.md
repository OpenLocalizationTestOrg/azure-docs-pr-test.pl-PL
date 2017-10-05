---
title: "Symulowane urządzenie & brama IoT Azure — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z IoT bramy Starter Kit, utworzenie Centrum Azure IoT i połączenia bramy z Centrum IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centrum Azure iot, bramy iot, wprowadzenie internet rzeczy, iot toolkit
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
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Rozpoczynanie pracy z IoT bramy Starter Kit z symulowane urządzenie

> [!div class="op_single_selector"]
> * [Sensor tag](iot-hub-gateway-kit-c-get-started.md)
> * [Symulowane urządzenie](iot-hub-gateway-kit-c-sim-get-started.md)

W tym samouczku, rozpoczyna się od podstawy pracy z uczenia [IoT bramy Starter Kit](https://aka.ms/gateway-kit). Będzie działać z NUC firmy Intel, z systemem Linux rzeki knie. Dowiesz się jak do seamleesly łączyć urządzenia do chmury przy użyciu Centrum IoT Azure.

***
**Zestaw nie ma jeszcze?:** kliknij [tutaj](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Lekcja 1. Konfigurowanie urządzenia NUC
![Diagram end-to-end Lesson1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

W tej lekcji Konfigurowanie NUC firmy Intel (dalej jednostki z przetwarzania danych) w zestawie jako bramy usługi Azure IoT, zainstaluj pakiet Azure IoT Edge na NUC i uruchom przykładową aplikację, aby sprawdzić funkcjonalność bramy.

*Szacowany czas trwania: 15 minut*

Przejdź do [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lekcja 2. Tworzenie centrum IoT Hub
![Diagram end-to-end Lesson2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

W tej lekcji należy zainstalować narzędzia i oprogramowania na komputerze hosta. Następnie możesz utworzyć bezpłatne konto platformy Azure, udostępnić Centrum Azure IoT i utworzyć pierwszego urządzenia w Centrum IoT.

Lekcja 1 należy wykonać przed rozpoczęciem tej lekcji.

### <a name="get-the-tools"></a>Uzyskaj narzędzia
Zainstaluj narzędzia i oprogramowania na komputerze hosta.

*Szacowany czas trwania: 20 minut*

Przejdź do [narzędzia](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Tworzenie Centrum IoT i rejestrowanie urządzenia
Tworzenie grupy zasobów, obsługi administracyjnej pierwszego Centrum Azure IoT i dodać pierwszego urządzenia do Centrum IoT przy użyciu wiersza polecenia platformy Azure.

*Szacowany czas trwania: 10 minut*

Przejdź do [tworzenia Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a>Lekcja 3: Odbieranie komunikatów z symulowane urządzenie i odbieranie wiadomości z Centrum IoT
W tej lekcji użyjesz skryptów do automatyzacji konfiguracji i wykonywania aplikacji symulowane urządzenie w Centrum. Aplikacja symulowane urządzenie generuje przykładowych danych temperatury i wysyła go do modułu Centrum IoT. Moduł Centrum IoT pakietów otrzymanych danych i wysyła go do Centrum IoT przez strukturę bramy w Azure IoT krawędzi.

![Diagram end-to-end Lekcja 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Konfigurowanie i uruchamianie symulowane urządzenie
Przygotuj przykładowych kodów. Następnie skonfiguruj i uruchom przykładową aplikację symulowane urządzenie.

*Szacowany czas trwania: 15 minut*

Przejdź do [Konfigurowanie i uruchamianie symulowane urządzenie](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT
Przykładowy kod należy uruchomić na komputerze hosta, aby odczytać wiadomości z Centrum IoT.

*Szacowany czas trwania: 15 minut*

Przejdź do [odczytywać wiadomości z Centrum IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-to-azure-table-storage"></a>Lekcja 4. Zapisywanie komunikatów w usłudze Azure Table Storage
Utwórz aplikację Azure funkcja, która pobiera komunikaty przychodzące z Centrum IoT i zapisuje je do magazynu tabel Azure.

![Diagram end-to-end lekcji 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure
Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage.

*Szacowany czas trwania: 10 minut*

Przejdź do [utworzyć konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure
Monitorowanie wiadomości bramy do chmury, ponieważ są one zapisywane do magazynu tabel Azure.

*Szacowany czas trwania: 5 minut*

Przejdź do [odczytywanie wiadomości utrwalane w magazynie tabel Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli masz problemy podczas wnioski Szukaj rozwiązań w [Rozwiązywanie problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) artykułu.

## <a name="explore-more"></a>Dowiedz się więcej
Odwiedź stronę [strefy developer Kit bramy IoT Intel](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) Aby dowiedzieć się więcej.