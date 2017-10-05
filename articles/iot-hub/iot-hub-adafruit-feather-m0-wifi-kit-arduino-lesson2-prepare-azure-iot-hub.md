---
title: "Nawiązać Arduino Azure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Adafruit piór M0 sieci Wi-Fi w Centrum Azure IoT za pomocą wiersza polecenia platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Łączenie arduino z chmury, Centrum azure iot, internet rzeczy chmury azure iot Centrum Utwórz urządzenie, arduino chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Utworzenie Centrum IoT i zarejestruj tablicy Adafruit piór M0 sieci Wi-Fi Arduino

## <a name="what-you-will-do"></a>Będzie wykonywać
* Utwórz grupę zasobów.
* Utworzenie Centrum Azure IoT w grupie zasobów.
* Dodaj tablicy Arduino do Centrum Azure IoT przy użyciu interfejsu wiersza polecenia platformy Azure (Azure CLI).

Korzystając z wiersza polecenia platformy Azure można dodać tablicy Arduino do Centrum IoT, Usługa generuje klucz dla tablicy Arduino do uwierzytelniania w usłudze. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshoot].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.
* Jak utworzyć tożsamość urządzenia dla tablicy Arduino w Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne
* Konto platformy Azure
* Komputer z wiersza polecenia platformy Azure zainstalowany

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
> Nazwa centrum IoT musi być globalnie unikatowa.
> Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Zarejestruj tablicy Arduino w Centrum IoT
Poszczególne urządzenia, która wysyła komunikaty do Centrum IoT i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.

Zarejestruj tablicy Arduino w Centrum IoT przez uruchomione następujące polecenie:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Podsumowanie
Utworzeniu Centrum IoT i zarejestrowane tablicy Arduino za pomocą tożsamości urządzenia w Centrum IoT. Możesz dowiedzieć się, jak wysyłać wiadomości z tablicy Arduino do Centrum IoT.

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji funkcji platformy Azure i konta magazynu Azure do przetwarzania i przechowywania wiadomości Centrum IoT][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md