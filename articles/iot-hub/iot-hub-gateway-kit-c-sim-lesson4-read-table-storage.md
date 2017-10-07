---
title: "Symulowane urządzenie & Azure IoT bramy - 4 lekcji: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Centrum IoT tooyour Intel NUC, zapisanie ich tooAzure tabeli magazynu, a następnie przeczytaj je z chmury hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Pobieranie danych z chmury, iot usługi w chmurze"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure

## <a name="what-you-will-do"></a>Będzie wykonywać

- Uruchom hello bramy przykładowej aplikacji na bramie wysyłanej wiadomości tooyour IoT hub.
- Uruchom przykładowy kod w wiadomości tooread hosta komputera w magazynie tabel Azure.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

Jak toouse hello system gulp narzędzie toorun przykładowy kod tooread wiadomości powitania w magazynie tabel Azure.

## <a name="what-you-need"></a>Co jest potrzebne

Został pomyślnie hello następujących zadań:

- [Utworzony hello Azure funkcji aplikacji i konto magazynu Azure hello](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).
- [Uruchom hello bramy przykładowej aplikacji](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).
- [Odbieranie wiadomości w Centrum IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Pobrać parametry połączenia magazynu Azure

Na początku tej lekcji pomyślnie utworzono konto magazynu platformy Azure. tooget hello parametry połączenia z kontem magazynu platformy Azure hello, uruchom następujące polecenia hello:

* Lista wszystkich kont magazynu.

```bash
az storage account list -g iot-gateway --query [].name
```

* Pobierz ciąg połączenia usługi azure storage.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Użyj `iot-gateway` jako wartość hello `{resource group name}` nie zmiany wartości hello Lekcja 2.

## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello

Aktualizacja hello `config-azure.json` plików, dzięki czemu hello przykładowy kod, który jest uruchamiany na komputerze hosta hello może odczytywać wiadomości w magazynie tabel Azure. tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:

1. Plik konfiguracji urządzenia Otwórz hello `config-azure.json` , uruchamiając następujące polecenia hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![konfiguracja](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Zastąp `[Azure storage connection string]` z hello parametry połączenia magazynu Azure uzyskany.

   `[IoT hub connection string]`już powinna zostać zastąpiona w sekcji [odczytywać wiadomości z Centrum IoT Azure](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) w Lesson3.

## <a name="read-messages-in-your-azure-table-storage"></a>Odczytywać wiadomości w magazynie tabel Azure

Uruchom hello bramy przykładowej aplikacji i odbieranie wiadomości magazynu tabel Azure przez hello następujące polecenie:

```bash
gulp run --table-storage
```

Centrum IoT wyzwala wiadomości toosave aplikacji funkcji platformy Azure do magazynu tabel Azure po odebraniu nowego komunikatu.
Witaj `gulp run` polecenie uruchamia aplikację przykładową bramy, która wysyła Centrum IoT tooyour wiadomości. Z `table-storage` parametru, jego również spowoduje utworzenie hello tooreceive procesu podrzędnego zapisać komunikatu w magazynie tabel Azure.

wiadomości powitania, które są wysyłane i odebranych znajdują się wszystkie wyświetlane natychmiast na powitania sam oknie w konsoli hello komputera-hosta. wystąpienie aplikacji przykładowej Hello zakończy się automatycznie w 40 sekund.

   ![Odczyt gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a>Podsumowanie

Uruchomiono wiadomości powitania tooread hello przykładowy kod w magazynie tabel Azure zapisane przez aplikację funkcji platformy Azure.
