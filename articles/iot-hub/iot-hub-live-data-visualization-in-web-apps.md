---
title: "dane o czasie aaaReal wizualizacji danych czujnika z Centrum Azure IoT — aplikacji sieci Web | Dokumentacja firmy Microsoft"
description: "Funkcja hello aplikacje sieci Web Microsoft Azure App Service toovisualize temperatury i wilgotności danych, który został zebrany z czujnika hello i wysyłany tooyour Centrum Iot."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "wizualizację danych czasu rzeczywistego, wizualizacji danych na żywo czujnik wizualizacji danych"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Wizualizacja danych czujnika w czasie rzeczywistym z Centrum Azure IoT za pomocą funkcji Web Apps hello Azure App Service

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Omawiane zagadnienia

Z tego samouczka dowiesz się, jak danych czujnika w czasie rzeczywistym toovisualize Centrum IoT odbieranych przez uruchomienie aplikacji sieci web, który znajduje się w aplikacji sieci web. Jeśli chcesz tootry toovisualize hello danych w Centrum IoT przy użyciu usługi Power BI, zobacz [danych czujnika w czasie rzeczywistym toovisualize usługi Power BI z Centrum IoT Azure](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>Co zrobić

- Tworzenie aplikacji sieci web w hello portalu Azure.
- Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.
- Skonfiguruj hello danych czujnika tooread aplikacji sieci web z Centrum IoT.
- Przekaż toobe aplikacji sieci web, na użytek hello aplikacji sieci web.
- Otwórz hello web toosee w czasie rzeczywistym temperatury i wilgotności danych aplikacji z Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- [Urządzenie jest skonfigurowane](iot-hub-raspberry-pi-kit-node-get-started.md), która obejmuje hello następujące wymagania:
  - Aktywną subskrypcją platformy Azure
  - Centrum Iot w ramach Twojej subskrypcji
  - Aplikacji klienckiej, która wysyła Centrum Iot tooyour wiadomości
- [Pobierz narzędzia Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web

1. W hello [portalu Azure](https://ms.portal.azure.com/), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.
2. Wprowadź nazwę unikatową zadania upewnij się, hello subskrypcji, określ grupę zasobów i lokalizację, wybierz opcję **toodashboard numeru Pin**, a następnie kliknij przycisk **Utwórz**.

   Zaleca się, że wybrano hello tej samej lokalizacji co dla Twojej grupy zasobów. W ten sposób mogą korzystać z szybkość przetwarzania i zmniejsza koszt hello transferu danych.

   ![Tworzenie aplikacji sieci Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Skonfiguruj hello dane tooread aplikacji sieci web z Centrum IoT

1. Otwórz aplikację sieci web hello, po prostu aprowizowanej.
2. Kliknij przycisk **ustawienia aplikacji**, a następnie w obszarze **ustawień aplikacji**, Dodaj następujące pary klucz wartość hello:

   | Klucz                                   | Wartość                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Uzyskane z Centrum iothub explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | Nazwa Hello grupy konsumentów hello dodanie tooyour Centrum IoT  |

   ![Dodawanie aplikacji sieci web tooyour ustawienia z pary klucz wartość](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Kliknij przycisk **ustawienia aplikacji**w obszarze **ustawienia ogólne**, Przełącz hello **sieci Web sockets** , a następnie kliknij przycisk **zapisać**.

   ![Przełącz hello opcja gniazda sieci Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Przekaż toobe aplikacji sieci web, na użytek hello aplikacji sieci web

W witrynie GitHub wprowadziliśmy dostępności aplikacji sieci web, który wyświetla danych czujnika w czasie rzeczywistym z Centrum IoT. Toodo wystarczy skonfigurować toowork aplikacji sieci web hello z repozytorium Git, Pobierz hello aplikacji sieci web z usługi GitHub i przekaż go po tooAzure dla toohost aplikacji sieci web hello.

1. W aplikacji sieci web hello, kliknij przycisk **opcje wdrażania** > **wybierz źródło** > **lokalnego repozytorium Git**, a następnie kliknij przycisk **OK**.

   ![Konfigurowanie sieci web aplikacji wdrożenia toouse hello lokalnego repozytorium Git](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Kliknij przycisk **poświadczenia wdrażania**, Utwórz użytkownika nazwę i hasło toouse tooconnect toohello repozytorium Git na platformie Azure, a następnie kliknij przycisk **zapisać**.

3. Kliknij przycisk **omówienie**i zanotuj wartość hello **adres url klonowania Git**.

   ![Pobierz adres URL klonowania Git hello aplikacji sieci web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Otwórz okno terminalu na komputerze lokalnym lub polecenie.

5. Pobierz aplikację sieci web hello z usługi GitHub i przekaż go tooAzure dla toohost aplikacji sieci web hello. toodo tak, uruchom następujące polecenia hello:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<Adres URL klonowania Git\> jest adres URL repozytorium Git hello na powitania hello **omówienie** strony hello aplikacji sieci web.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Otwórz hello web toosee w czasie rzeczywistym temperatury i wilgotności danych aplikacji z Centrum IoT

Na powitania **omówienie** strony aplikacji sieci web, kliknij przycisk aplikacji hello tooopen hello adres URL w sieci web.

![Pobieranie adresu URL hello aplikacji sieci web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Witaj w czasie rzeczywistym temperatury i wilgotności danych powinny być widoczne z Centrum IoT.

![Wyświetlanie w czasie rzeczywistym temperatury i wilgotności strony aplikacji sieci Web](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Upewnij się, że hello Przykładowa aplikacja jest uruchomiona na urządzeniu. Nie otrzymasz pusty wykres, może się odwoływać samouczki toohello w obszarze [skonfigurować na twoim urządzeniu](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Następne kroki
Pomyślnie zastosowano danych czujnika w czasie rzeczywistym toovisualize aplikacji sieci web z Centrum IoT.

Alternatywna metoda toovisualize danych z Centrum IoT Azure, zobacz [danych czujnika w czasie rzeczywistym toovisualize usługi Power BI z Centrum IoT](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
