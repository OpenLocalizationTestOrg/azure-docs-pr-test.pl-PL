---
title: "Symulowane urządzenie & Azure IoT bramy - lekcji 3: odczytywać wiadomości | Dokumentacja firmy Microsoft"
description: "Uruchom przykładowy kod w wiadomości powitania tooread komputera hosta z Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT

## <a name="what-you-will-do"></a>Będzie wykonywać

- Uruchom przykładowy kod na hoście komputer tooread komunikaty z Centrum IoT.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

Jak toouse hello system gulp narzędzie tooread komunikaty z Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Przykładowe symulowane urządzenie Hello w [Konfigurowanie i uruchamianie Chmury symulowane urządzenie przekazać przykładowej aplikacji](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT

ciąg połączenia urządzenia Hello jest używany przez Centrum IoT tooyour tooconnect symulowane urządzenie. Parametry połączenia Centrum IoT Hello jest rejestru tożsamości toohello tooconnect używanych w urządzeniami hello toomanage Centrum IoT, które są dozwolone Centrum IoT tooyour tooconnect.

- Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie hello:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Użyj `iot-gateway` jako wartość hello `{resource group name}` nie zostały wprowadzone zmiany.
- Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie hello:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`to nazwa hello określony Lekcja 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Skonfiguruj połączenie z urządzeniem hello hello przykładowy kod

Aktualizacja konfiguracji IoT hub i urządzenia połączenia w `config-azure.json` , wykonując następujące kroki hello:

1. Otwórz `config-azure.json` w programie Visual Studio Code, uruchamiając następujące polecenie w oknie konsoli hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Wprowadź następujące elementy zastępcze w hello hello `config-azure.json` pliku:

   ![Zrzut ekranu przedstawiający konfiguracji platformy azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Zastąp `[IoT hub connection string]` z hello parametry połączenia Centrum IoT.

## <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT

Uruchom hello symulowane urządzenie przykładowej aplikacji i odczytać Centrum IoT wiadomości powitania następujące polecenie:

```bash
gulp run --iot-hub
```

polecenie Hello uruchamia aplikacji hello, który wysyła wiadomości tooyour IoT hub co 2 sekundy. Spowoduje również utworzenie wiadomość hello tooreceive procesu podrzędnego.

wiadomości powitania, które są wysyłane i odebranych znajdują się wszystkie wyświetlane natychmiast na powitania sam oknie w konsoli hello komputera-hosta. Aplikacja Hello zakończy działanie w 40 sekund.

![Symulowane przykładową aplikację z wysłane i odebrane wiadomości](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Podsumowanie

Pomyślnie uruchomiono Centrum IoT tooyour danych toosend hello przykładowej aplikacji z symulowanego urządzenia. Wiadomości powitania, które zostały wysłane do Centrum IoT tooyour również zostały przeczytane.

## <a name="next-steps"></a>Następne kroki
[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md) (Tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage)


