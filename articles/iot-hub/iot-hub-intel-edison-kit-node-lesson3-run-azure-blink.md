---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — lekcji 3: wysyłanie komunikatów | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowych aplikacji tooIntel Edison, która wysyła Centrum IoT tooyour wiadomości i miganie hello LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania toocloud danych"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury
## <a name="what-you-will-do"></a>Będzie wykonywać
W tym artykule opisano sposób toodeploy i uruchom przykładową aplikację na Edison firmy Intel, który wysyła wiadomości tooyour Centrum IoT. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-learn"></a>Co dowiesz się
Zostanie Dowiedz się, jak toouse hello system gulp toodeploy narzędzie i uruchom hello przykładowej aplikacji C dla Edison.

## <a name="what-you-need"></a>Co jest potrzebne
* Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenie aplikacji funkcji platformy Azure i magazynu konta tooprocess i Magazyn Centrum IoT wiadomości][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT
Parametry połączenia urządzenia Hello są używane tooconnect Centrum IoT tooyour Edison. Parametry połączenia Centrum IoT Hello jest używany tooconnect tożsamości IoT hub toohello urządzenia reprezentujący Edison w Centrum IoT hello.

* Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.

* Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`to nazwa hello określone podczas tworzenia Centrum IoT i zarejestrowana Edison.

* Pobierz ciąg połączenia urządzenia hello, uruchamiając następujące polecenie hello:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Użyj `myinteledison` jako wartość hello `{device id}` Jeśli hello wartość nie zostanie zmieniona.

## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello
1. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   npm install
   gulp init
   ```

2. Plik konfiguracji urządzenia Otwórz hello `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. Wprowadź następujące elementy zastępcze w hello hello `config-edison.json` pliku:

   * Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia hello oznaczone w dół, podczas konfigurowania urządzenia.
   * Zastąp **[parametry połączenia urządzenia IoT]** z hello `device connection string` uzyskaną.
   * Zastąp **[parametry połączenia Centrum IoT]** z hello `iot hub connection string` uzyskaną.

   > [!NOTE]
   > Nie ma potrzeby `azure_storage_connection_string` w tym artykule. Zachować, ponieważ jest.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na Edison, uruchamiając następujące polecenie hello:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Sprawdź, czy działa hello przykładowej aplikacji
Powinny pojawić się hello LED, który jest połączony tooEdison migający co dwie sekundy. Za każdym razem, gdy hello LED miga, hello przykładowej aplikacji wysyła z Centrum IoT tooyour wiadomości i sprawdza, czy tę wiadomość hello została pomyślnie wysłana tooyour Centrum IoT. Ponadto każdy komunikat odebrany przez Centrum IoT hello jest drukowany w oknie konsoli hello. Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu wiadomości 20.

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Podsumowanie
Została wdrożona i uruchom hello nowe migania przykładowej aplikacji na Edison Centrum IoT tooyour wiadomości urządzenia do chmury toosend. Jak są one zapisywane na koncie magazynu toohello teraz monitorować wiadomości.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md