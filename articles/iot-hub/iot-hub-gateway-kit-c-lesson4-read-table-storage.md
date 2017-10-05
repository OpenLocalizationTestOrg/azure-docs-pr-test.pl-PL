---
title: "Urządzeń Sensor tag & bramy IoT Azure - lekcja 4: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Intel NUC do Centrum IoT, zapisanie ich do magazynu tabel Azure, a następnie przeczytaj je z chmury."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Pobieranie danych z chmury, iot usługi w chmurze"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 72659ef3a7fd2f6011590d37176fd05503269aff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure

## <a name="what-you-will-do"></a>Będzie wykonywać

- Uruchom przykładową aplikację bramy dla bramy wysyłania komunikatów do Centrum IoT.
- Następnie uruchom przykładowy kod na komputerze hosta odczytywać wiadomości z magazynem tabel Azure. 

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

Jak używać narzędzia gulp uruchamiać kod przykładowy można odczytywać wiadomości w magazynie tabel Azure.

## <a name="what-you-need"></a>Co jest potrzebne

Został pomyślnie wykonać następujące zadania:

- [Utworzone konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Uruchom przykładową aplikację bramy](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [Odbieranie wiadomości w Centrum IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Pobrać parametry połączenia magazynu Azure

Na początku tej lekcji pomyślnie utworzono konto magazynu platformy Azure. Można pobrać ciągu połączenia z kontem magazynu platformy Azure, uruchom następujące polecenia:

* Lista wszystkich kont magazynu.

```bash
az storage account list -g iot-gateway --query [].name
```

* Pobierz ciąg połączenia usługi azure storage.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Użyj bramy iot jako wartość `{resource group name}` nie zmiany wartości Lekcja 2.

## <a name="configure-the-device-connection"></a>Skonfiguruj połączenie z urządzeniem

Aktualizacja `config-azure.json` plików, dzięki czemu przykładowy kod, który jest uruchamiany na komputerze hosta może odczytywać wiadomości w magazynie tabel Azure. Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:

1. Otwórz plik konfiguracji urządzenia `config-azure.json` , uruchamiając następujące polecenia:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![konfiguracja](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Zastąp `[Azure storage connection string]` przy użyciu parametrów połączenia magazynu Azure uzyskany.

   `[IoT hub connection string]`już powinna zostać zastąpiona w sekcji [odczytywać wiadomości z Centrum IoT Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) w Lesson3.

## <a name="read-messages-in-your-azure-table-storage"></a>Odczytywać wiadomości w magazynie tabel Azure

Uruchom przykładową aplikację bramy i odbieranie wiadomości magazynu tabel Azure za pomocą następującego polecenia:

```bash
gulp run --table-storage
```

Centrum IoT wyzwala aplikacji funkcji platformy Azure do zapisywania wiadomości do magazynu tabel Azure po odebraniu nowego komunikatu.
`gulp run` Polecenie uruchamia aplikację przykładową bramy, która wysyła komunikaty do Centrum IoT. Z `table-storage` parametru, jego również spowoduje utworzenie proces podrzędny komunikat zapisane w magazynie tabel Azure.

Komunikaty, które są wysyłane i odebranych są wszystkie natychmiast wyświetlane na tym samym oknie konsoli w komputerze hosta. Wystąpienie aplikacji przykładowej zakończy się automatycznie w 40 sekund.

   ![Odczyt gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Podsumowanie

Uruchomiono przykładowy kod umożliwiający odczytywać wiadomości z magazynem tabel Azure zapisane przez aplikację funkcji platformy Azure.