---
featureFlags: usabilla
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Pi w rejestrze tożsamości Centrum IoT przy użyciu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Utworzenie Centrum IoT i zarejestruj malina Pi 3
## <a name="what-you-will-do"></a>Będzie wykonywać
* Utwórz grupę zasobów.
* Utworzenie Centrum Azure IoT w grupie zasobów.
* Dodaj malina Pi 3 do Centrum Azure IoT przy użyciu interfejsu wiersza polecenia platformy Azure (Azure CLI).

Korzystając z wiersza polecenia platformy Azure można dodać Pi do Centrum IoT, Usługa generuje klucz pi do uwierzytelniania w usłudze. Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT
* Jak utworzyć tożsamość urządzenia pi w Centrum IoT

## <a name="what-you-need"></a>Co jest potrzebne
* Konto platformy Azure
* Mac lub komputerze z systemem Windows z wiersza polecenia platformy Azure zainstalowany

## <a name="create-your-iot-hub"></a>Utworzenie Centrum IoT
Centrum IoT Azure pomaga połączyć, monitorować i zarządzać nimi miliony zasoby IoT. Aby utworzyć Centrum IoT, wykonaj następujące kroki:

1. Zaloguj się do konta platformy Azure, uruchamiając następujące polecenie:

   ```bash
   az login
   ```

   Wszystkie dostępne subskrypcje są wyświetlane po pomyślnym zalogowaniu.

2. Wartość domyślna subskrypcja, którego chcesz używać, uruchamiając następujące polecenie:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`można znaleźć w danych wyjściowych `az login` lub `az account list` polecenia.

3. Zarejestruj dostawcę, uruchamiając następujące polecenie. Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji. Przed wdrożeniem zasobów platformy Azure, dostawcy oferujący należy zarejestrować dostawcę.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Utwórz grupę zasobów o nazwie iot próbkami regionu zachodnie stany USA, uruchamiając następujące polecenie:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`jest to lokalizacja, tworzenie grupy zasobów. Jeśli chcesz użyć innej lokalizacji, możesz uruchomić `az account list-locations -o table` do wyświetlenia wszystkich lokalizacji platformy Azure obsługuje.
 
5. Utwórz Centrum IoT w grupie zasobów przykładowej iot, uruchamiając następujące polecenie:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   Domyślnie narzędzie tworzy Centrum IoT w warstwy cenowej bezpłatna. Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE] 
> Nazwa centrum IoT musi być globalnie unikatowa. Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.

## <a name="register-pi-in-your-iot-hub"></a>Zarejestruj Pi w Centrum IoT
Poszczególne urządzenia, która wysyła komunikaty do Centrum IoT i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora. Azure CLI użyje do rejestracji programu Pi i utwórz samopodpisany certyfikat X.509 do uwierzytelniania urządzeń.

Uruchom następujące polecenie:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Podsumowanie
Utworzeniu Centrum IoT i zarejestrowane Pi za pomocą tożsamości urządzenia w Centrum IoT. Możesz dowiedzieć się, jak wysyłać wiadomości z Pi do Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure do przetwarzania i przechowywania wiadomości Centrum IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

