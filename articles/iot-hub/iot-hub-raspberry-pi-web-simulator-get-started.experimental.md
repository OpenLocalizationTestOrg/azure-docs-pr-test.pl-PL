---
title: "aaaSimulated Pi malina toocloud (Node.js) - tooAzure symulatora web Pi malina połączenia Centrum IoT | Dokumentacja firmy Microsoft"
description: "Połączenia sieci web Pi malina symulatora tooAzure Centrum IoT dla Pi malina toosend danych toohello chmury Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi malinowe symulatora azure iot malinowe pi malinowe pi Centrum iot, malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Połącz tooAzure online symulatora Pi malina Centrum IoT (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

W tym samouczku Rozpocznij od uczenia hello podstawy pracy z Pi malina symulatora online. Następnie dowiesz się, jak połączyć tooseamlessly hello Pi symulatora toohello chmury za pomocą [Centrum IoT Azure](iot-hub-what-is-iot-hub.md). 

Jeśli masz urządzenia fizyczne, odwiedź stronę [tooAzure połączyć Pi malina Centrum IoT](iot-hub-raspberry-pi-kit-node-get-started.md) tooget uruchomiona. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>Co zrobić

* Dowiedz się hello podstawy Pi malina symulatora online.
* Tworzenie Centrum IoT.
* Zarejestruj urządzenie pi w Centrum IoT.
* Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika toosend symulowane Pi.

Połącz symulowane Pi malina tooan Centrum IoT utworzony. Następnie uruchom przykładową aplikację z danych czujnika toogenerate symulatora hello. Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.

## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Jak toowork z symulatorem online malina Pi.
* Jak Centrum IoT tooyour danych czujnika toosend.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Omówienie symulatora web Pi malina

Kliknij przycisk hello przycisk toolaunch Pi malina online symulatora.

> [!div class="button"]
[Uruchomić symulatora Pi malina](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Istnieją trzy obszary w symulatorze web hello.
* Obszar zestawu — hello domyślne obwód jest, że Pi nawiązanie połączenia z czujnika BME280 i LED. obszar Hello jest zablokowany w wersji preview tak aktualnie nie może wykonać dostosowania.
* Kodowanie obszar — edytora online kodu dla toocode z malina Pi. Hello domyślne przykładowej aplikacji ułatwia toocollect danych czujnika z czujnika BME280 i wysyła tooyour Centrum IoT Azure. Aplikacja Hello jest w pełni zgodny z rzeczywistych urządzeń Pi. 
* Okno konsoli zintegrowane - zawiera dane wyjściowe hello kodu. U góry hello tego okna istnieją trzy przyciski.
   * **Uruchom** -uruchamiania aplikacji hello w hello kodowania obszaru.
   * **Resetuj** -kodowania obszaru toohello domyślne Przykładowa aplikacja hello resetowania.
   * **Składanie/rozszerzanie** — na powitania prawej stronie jest przycisk dla można rozwinąć/toofold hello okna konsoli.

> [!NOTE] 
Symulator web Pi malina Hello jest teraz dostępna w wersji zapoznawczej. Chcielibyśmy toohear głosu w hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator). Kod źródłowy Hello jest publiczny na [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Omówienie Pi symulatora online](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Uruchom przykładową aplikację w symulatorze web Pi

1. W kodowania obszaru, upewnij się, że pracujesz na powitania domyślne przykładowej aplikacji. Zastąp symbol zastępczy hello w wierszu 15 hello ciąg połączenia urządzenia Centrum Azure IoT.
   ![Zastąp ciąg połączenia urządzenia hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Kliknij przycisk **Uruchom** lub typ `npm start` toorun hello aplikacji.


Powinny pojawić się hello następujące dane wyjściowe, który zawiera dane czujników hello i wiadomości powitania, które są wysyłane z Centrum IoT tooyour ![dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Następne kroki

Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
