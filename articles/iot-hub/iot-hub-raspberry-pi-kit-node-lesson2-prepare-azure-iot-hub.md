---
featureFlags: usabilla
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Pi w hello Centrum IoT rejestru tożsamości za pomocą wiersza polecenia platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Połącz chmury pi malinowe pi chmury,"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Utworzenie Centrum IoT i zarejestruj malina Pi 3
## <a name="what-you-will-do"></a>Będzie wykonywać
* Utwórz grupę zasobów.
* Utworzenie Centrum Azure IoT w grupie zasobów hello.
* Dodaj Centrum Azure IoT toohello malina Pi 3 za pomocą hello interfejsu wiersza polecenia platformy Azure (Azure CLI).

Korzystając z Centrum IoT tooyour Pi tooadd wiersza polecenia platformy Azure, usługa hello generuje klucz dla tooauthenticate Pi z usługą hello. Jeśli masz problemy z poszukiwanie rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak toouse toocreate interfejsu wiersza polecenia Azure IoT hub
* Jak toocreate tożsamość urządzenia pi w Centrum IoT

## <a name="what-you-need"></a>Co jest potrzebne
* Konto platformy Azure
* Mac lub komputerze z systemem Windows z hello Azure CLI jest zainstalowany

## <a name="create-your-iot-hub"></a>Utworzenie Centrum IoT
Centrum IoT Azure pomaga połączyć, monitorować i zarządzać nimi miliony zasoby IoT. toocreate Centrum IoT, wykonaj następujące kroki:

1. Zaloguj się tooyour konto platformy Azure, uruchamiając następujące polecenie hello:

   ```bash
   az login
   ```

   Wszystkie dostępne subskrypcje są wyświetlane po pomyślnym zalogowaniu.

2. Ustaw hello Domyślna subskrypcja ma toouse, uruchamiając następujące polecenie hello:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`można znaleźć w danych wyjściowych hello hello `az login` lub hello `az account list` polecenia.

3. Zarejestruj dostawcę hello, uruchamiając następujące polecenie hello. Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji. Należy zarejestrować dostawcę hello przed wdrożeniem hello zasobów platformy Azure, która hello oferty dostawcy.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Utwórz grupę zasobów o nazwie na próbki iot, hello regionu zachodnie stany USA, uruchamiając następujące polecenie hello:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`to miejsce hello Tworzenie grupy zasobów. Jeśli chcesz toouse w innej lokalizacji, możesz uruchomić `az account list-locations -o table` toosee wszystkie hello Azure obsługuje lokalizacji.
 
5. Utwórz Centrum IoT w grupie zasobów przykładowej iot hello, uruchamiając następujące polecenie hello:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   Domyślnie narzędzie hello tworzy Centrum IoT w hello warstwa cenowa bezpłatna. Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE] 
> Hello nazwę Centrum IoT musi być globalnie unikatowa. Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.

## <a name="register-pi-in-your-iot-hub"></a>Zarejestruj Pi w Centrum IoT
Poszczególne urządzenia, która Centrum IoT tooyour komunikatów wysyła i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora. Zostanie Użyj interfejsu wiersza polecenia Azure tooregister Twojego Pi i utwórz samopodpisany certyfikat X.509 do uwierzytelniania urządzeń.

Uruchom następujące polecenie hello:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Podsumowanie
Utworzeniu Centrum IoT i zarejestrowane Pi za pomocą tożsamości urządzenia w Centrum IoT. Wszystko jest gotowe toolearn jak toosend komunikaty z Centrum IoT tooyour Pi.

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji funkcji platformy Azure i tooprocess konta magazynu platformy Azure i przechowywania komunikatów Centrum IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

