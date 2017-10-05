---
title: "Connect Intel Edison (C) do Azure IoT — lekcji 3: wysyłanie komunikatów | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowej aplikacji do Edison firmy Intel, który wysyła wiadomości do Centrum IoT i miganie LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania danych do chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d104618ebb37a19c83f161beceb5c71bc89bbb56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury
## <a name="what-you-will-do"></a>Będzie wykonywać
W tym artykule opisano sposób wdrażania i uruchom przykładową aplikację na Edison firmy Intel, który wysyła wiadomości do Centrum IoT. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
Zostanie sposób użycia narzędzia gulp do wdrożenia i uruchomienia przykładowej aplikacji C na Edison.

## <a name="what-you-need"></a>Co jest potrzebne
* Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenia aplikacji funkcji platformy Azure i konto magazynu do przetwarzania i przechowywania wiadomości Centrum IoT][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT
Ciąg połączenia urządzenia jest używany do nawiązania Edison Centrum IoT. Parametry połączenia Centrum IoT jest używany do nawiązania połączenia tożsamości tego urządzenia, który reprezentuje Edison w Centrum IoT Centrum IoT.

* Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.

* Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`jest to nazwa określona podczas tworzenia Centrum IoT i zarejestrowana Edison.

* Pobierz ciąg połączenia urządzenia, uruchamiając następujące polecenie:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Użyj `myinteledison` jako wartość `{device id}` Jeśli wartości nie można zmienić.

## <a name="configure-the-device-connection"></a>Skonfiguruj połączenie z urządzeniem
1. Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.

2. Otwórz plik konfiguracji urządzenia `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. Wprowadź następujące elementy zastępcze w `config-edison.json` pliku:

   * Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia, które są oznaczone w dół, podczas konfigurowania urządzenia.
   * Zastąp **[parametry połączenia urządzenia IoT]** z `device connection string` uzyskaną.
   * Zastąp **[parametry połączenia Centrum IoT]** z `iot hub connection string` uzyskaną.

   > [!NOTE]
   > Nie ma potrzeby `azure_storage_connection_string` w tym artykule. Zachować, ponieważ jest.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na Edison, uruchamiając następujące polecenie:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Sprawdź, czy działa przykładowej aplikacji
Powinny pojawić się LED, która jest połączona z Edison migający co dwie sekundy. Za każdym razem, gdy LED miga, przykładowej aplikacji wysyła komunikat do Centrum IoT i sprawdza, czy wiadomość została pomyślnie wysłana do Centrum IoT. Ponadto każdy komunikat odebrany przez Centrum IoT jest drukowany w oknie konsoli. Przykładowa aplikacja kończy się automatycznie po wysłaniu wiadomości 20.

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Podsumowanie
Został wdrożony i Uruchom nowe migania przykładową aplikację na Edison do wysyłania wiadomości urządzenia do chmury do Centrum IoT. Wiadomości jest teraz monitorować, ponieważ są one zapisywane na koncie magazynu.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md