---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Centrum Azure iot, internet rzeczy chmury azure iot Centrum tworzenia urządzenia, analizy czasowej Sensor tag, cz analizy czasowej"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Utworzenie Centrum Azure IoT i rejestrowanie urządzenia

## <a name="what-you-will-do"></a>Będzie wykonywać

- Tworzenie grupy zasobów
- Utworzenie pierwszego Centrum IoT
- Zarejestruj urządzenie w Centrum IoT przy użyciu hello wiersza polecenia platformy Azure. 

Po zarejestrowaniu urządzenia w Centrum IoT hello usługi Centrum IoT Azure generuje klucz dla tooauthenticate toouse Twojego urządzenia z usługą hello. 

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.
- Jak tooregister urządzenie w Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.
- Powinien mieć hello zainstalowana wiersza polecenia platformy Azure.

## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT

toocreate Centrum IoT, wykonaj następujące kroki:

1. Zaloguj się tooyour konto platformy Azure, uruchamiając następujące polecenie hello:

   ```bash
   az login
   ```

   Zostaną wyświetlone wszystkie subskrypcje dostępne po pomyślnym zalogowaniu.

2. Ustaw domyślny hello subskrypcji platformy Azure, które mają toouse, uruchamiając następujące polecenie hello:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`można znaleźć w danych wyjściowych hello hello `az login` lub hello `az account list` polecenia.

3. Zarejestruj dostawcę hello, uruchamiając następujące polecenie hello. Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji. Należy zarejestrować dostawcę hello przed wdrożeniem hello zasobów platformy Azure, która hello oferty dostawcy.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Utwórz grupę zasobów o nazwie `iot-gateway` hello regionu zachodnie stany USA, uruchamiając następujące polecenie hello:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`to miejsce hello Tworzenie grupy zasobów. Jeśli chcesz toouse w innej lokalizacji, możesz uruchomić `az account list-locations -o table` toosee wszystkie hello Azure obsługuje lokalizacji.

5. Tworzenie Centrum IoT w hello `iot-gateway` grupy zasobów, uruchamiając następujące polecenie hello:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Domyślnie narzędzie hello tworzy Centrum IoT w hello warstwa cenowa bezpłatna. Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> Hello nazwę Centrum IoT musi być globalnie unikatowa. Można utworzyć tylko jedną F1 wersji Centrum Iot Azure w ramach Twojej subskrypcji platformy Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Zarejestruj urządzenie w Centrum IoT

Poszczególne urządzenia, która Centrum IoT tooyour komunikatów wysyła i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.
Zarejestruj urządzenie w Centrum IoT przez uruchomione następujące polecenie:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Podsumowanie

Utworzeniu Centrum IoT i zarejestrowane urządzenia logicznego za pomocą tożsamości urządzenia w Centrum IoT. Wszystko jest gotowe toolearn jak tooconfigure i uruchamiania bramy przykładowych aplikacji toosend danych z urządzenia fizycznego Centrum IoT tooyour w hello chmury.

## <a name="next-steps"></a>Następne kroki
[Konfigurowanie i uruchamianie cz przykładową aplikację](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)