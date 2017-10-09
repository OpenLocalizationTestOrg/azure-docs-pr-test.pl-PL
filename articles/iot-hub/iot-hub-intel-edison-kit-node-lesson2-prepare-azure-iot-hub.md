---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Edison w Centrum Azure IoT hello za pomocą hello wiersza polecenia platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a70cd8d6a6d620a2cf6226397e061af6cf81e0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>Utworzenie Centrum IoT i zarejestruj Intel Edison
## <a name="what-you-will-do"></a>Będzie wykonywać
* Utwórz grupę zasobów.
* Utworzenie Centrum Azure IoT w grupie zasobów hello.
* Dodaj Centrum Azure IoT toohello Intel Edison przy użyciu hello interfejsu wiersza polecenia platformy Azure (Azure CLI).

Gdy używasz hello Azure CLI tooadd Centrum IoT tooyour Edison usługi hello generuje klucz dla tooauthenticate Edison z usługą hello. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.
* Jak toocreate tożsamość urządzenia dla Edison w Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne
* Konto platformy Azure. Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.
* Powinien mieć hello zainstalowana wiersza polecenia platformy Azure.

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
> Hello nazwę Centrum IoT musi być globalnie unikatowa.
> Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.


## <a name="register-edison-in-your-iot-hub"></a>Zarejestruj Edison w Centrum IoT
Poszczególne urządzenia, która Centrum IoT tooyour komunikatów wysyła i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.

Zarejestruj Edison w Centrum IoT przez uruchomione następujące polecenie:

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Podsumowanie
Utworzeniu Centrum IoT i zarejestrowane Edison za pomocą tożsamości urządzenia w Centrum IoT. Wszystko jest gotowe toolearn jak toosend komunikaty z Centrum IoT tooyour Edison.

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji funkcji platformy Azure i usługi Azure Storage konta tooprocess i Magazyn Centrum IoT wiadomości][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md