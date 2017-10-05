---
title: "Symulowane urządzenie & Azure IoT brama - 2 lekcji: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Centrum Azure iot, internet rzeczy chmury azure iot Centrum tworzenia urządzenia, analizy czasowej Sensor tag, cz analizy czasowej"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5557989453eb47e4c3a287b26603eff040eb1d96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Utworzenie Centrum Azure IoT i rejestrowanie urządzenia

## <a name="what-you-will-do"></a>Będzie wykonywać

- Tworzenie grupy zasobów
- Utworzenie pierwszego Centrum IoT
- Zarejestruj urządzenie w Centrum IoT przy użyciu wiersza polecenia platformy Azure. 

Podczas rejestrowania urządzenia w Centrum IoT, usługa Azure IoT Hub generuje klucz dla urządzenia w celu używania do uwierzytelniania w usłudze. 

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.
- Jak zarejestrować urządzenie w Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.
- Powinny mieć zainstalowane interfejsu wiersza polecenia Azure.

## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT

Aby utworzyć Centrum IoT, wykonaj następujące kroki:

1. Zaloguj się do konta platformy Azure, uruchamiając następujące polecenie:

   ```bash
   az login
   ```

   Zostaną wyświetlone wszystkie subskrypcje dostępne po pomyślnym zalogowaniu.

2. Ustaw domyślny subskrypcji Azure, która ma być używany, uruchamiając następujące polecenie:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`można znaleźć w danych wyjściowych `az login` lub `az account list` polecenia.

3. Zarejestruj dostawcę, uruchamiając następujące polecenie. Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji. Przed wdrożeniem zasobów platformy Azure, dostawcy oferujący należy zarejestrować dostawcę.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Utwórz grupę zasobów o nazwie `iot-gateway` regionu zachodnie stany USA, uruchamiając następujące polecenie:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`jest to lokalizacja, tworzenie grupy zasobów. Jeśli chcesz użyć innej lokalizacji, możesz uruchomić `az account list-locations -o table` do wyświetlenia wszystkich lokalizacji platformy Azure obsługuje.

5. Tworzenie Centrum IoT w `iot-gateway` grupy zasobów, uruchamiając następujące polecenie:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Domyślnie narzędzie tworzy Centrum IoT w warstwy cenowej bezpłatna. Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> Nazwa centrum IoT musi być globalnie unikatowa. Można utworzyć tylko jedną F1 wersji Centrum Iot Azure w ramach Twojej subskrypcji platformy Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Zarejestruj urządzenie w Centrum IoT

Poszczególne urządzenia, która wysyła komunikaty do Centrum IoT i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.
Zarejestruj urządzenie w Centrum IoT przez uruchomione następujące polecenie:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Podsumowanie

Utworzeniu Centrum IoT i zarejestrowane urządzenia logicznego za pomocą tożsamości urządzenia w Centrum IoT. Możesz dowiedzieć się, jak skonfigurować i uruchomić bramy przykładowej aplikacji do wysyłania danych z urządzenia fizycznego do Centrum IoT w chmurze.

## <a name="next-steps"></a>Następne kroki
[Konfigurowanie i uruchamianie symulowane urządzenie chmury przekazywania przykładowej aplikacji](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)