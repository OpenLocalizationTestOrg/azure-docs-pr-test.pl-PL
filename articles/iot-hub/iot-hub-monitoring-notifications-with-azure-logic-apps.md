---
title: "zdalne monitorowanie aaaIoT i powiadomienia przy użyciu usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Logic Apps IoT temperatury monitorowania w Centrum IoT i automatycznie wysyłać skrzynki pocztowej tooyour powiadomienia e-mail dla wszelkich wykrytych nieprawidłowości."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: monitorowanie powiadomienia iot iot monitorowania temperatury iot
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Zdalne monitorowanie IoT i powiadomienia przy użyciu usługi Azure Logic Apps łączenia z Centrum IoT i skrzynek pocztowych

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Aplikacje logiki platformy Azure umożliwia procesów tooautomate jako serię kroków. Aplikacja logiki mogą się łączyć przez różnych usług i protokołów. Rozpoczyna się wyzwalacz takich jak "Po dodaniu konta" i następuje kombinacją akcji, jak "wysyła powiadomienie wypychane". Ta funkcja umożliwia Logic Apps to idealne rozwiązanie IoT dla IoT monitorowania, takich jak pozostaje alert w celu wykrycia nieprawidłowości, między innymi scenariusze użycia.

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiesz się, jak toocreate aplikacji logiki łączącej centrum IoT i skrzynki pocztowej temperatury monitorowania i powiadomień. Gdy temperatury hello jest ponad 30 C, hello znaczniki aplikacji klienta `temperatureAlert = "true"` w wiadomości powitania wysyła tooyour Centrum IoT. wiadomości powitania wyzwalaczy hello toosend aplikacji logiki możesz wiadomość e-mail z powiadomieniem.

## <a name="what-you-do"></a>Co zrobić

* Utwórz przestrzeń nazw magistrali usług i Dodaj tooit kolejki.
* Dodawanie punktu końcowego i routingu Centrum IoT tooyour reguły.
* Tworzenie, konfigurowanie i testowanie aplikacji logiki.

## <a name="what-you-need"></a>Co jest potrzebne

* Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:
  * Aktywna subskrypcja platformy Azure.
  * Centrum Azure IoT w ramach Twojej subskrypcji.
  * Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Utwórz przestrzeń nazw magistrali usług i Dodaj tooit kolejki

### <a name="create-a-service-bus-namespace"></a>Utwórz przestrzeń nazw magistrali usług

1. Na powitania [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **integracji przedsiębiorstwa** > **usługi Service Bus**.
1. Podaj hello następujących informacji:

   **Nazwa**: Nazwa hello hello service Bus.

   **Warstwa cenowa**: kliknij **podstawowe** > **wybierz**. Warstwa podstawowa Hello jest wystarczająca dla tego samouczka.

   **Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.

   **Lokalizacja**: Użyj hello sam lokalizacji, która korzysta z Centrum IoT.
1. Kliknij przycisk **Utwórz**.

   ![Utwórz przestrzeń nazw magistrali usług w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Dodaj kolejką usługi service bus

1. Otwórz hello przestrzeń nazw magistrali usług, a następnie kliknij przycisk **+ kolejki**.
1. Wprowadź nazwę kolejki hello, a następnie kliknij przycisk **Utwórz**.
1. Otwórz hello kolejką usługi service bus, a następnie kliknij przycisk **zasady dostępu współużytkowanego** > **+ Dodaj**.
1. Wprowadź nazwę zasady hello wyboru **Zarządzaj**, a następnie kliknij przycisk **Utwórz**.

   ![Dodaj kolejką usługi service bus w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Dodawanie punktu końcowego i routingu Centrum IoT tooyour reguły

### <a name="add-an-endpoint"></a>Dodawanie punktu końcowego

1. Otwórz Centrum IoT, kliknij punkty końcowe > + Dodaj.
1. Wprowadź hello następujących informacji:

   **Nazwa**: hello Nazwa punktu końcowego hello.

   **Typ punktu końcowego**: Wybierz **kolejką usługi Service Bus**.

   **Przestrzeń nazw magistrali usług**: Wybierz nazw hello został utworzony.

   **Kolejki usługi Service Bus**: kolejki hello wybierz utworzony.
1. Kliknij przycisk **OK**.

   ![Dodawanie punktu końcowego Centrum IoT tooyour w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Dodaj regułę routingu

1. W Centrum IoT kliknij **tras** > **+ Dodaj**.
1. Wprowadź hello następujących informacji:

   **Nazwa**: hello nazwa hello reguły routingu.

   **Źródło danych**: Wybierz **DeviceMessages**.

   **Punkt końcowy**: Wybierz hello punkt końcowy został utworzony.

   **Długość ciągu zapytania**: wprowadź `temperatureAlert = "true"`.
1. Kliknij pozycję **Zapisz**.

   ![Dodaj regułę routingu w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Tworzenie i konfigurowanie aplikacji logiki

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki

1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **integracji przedsiębiorstwa** > **aplikacji logiki**.
1. Wprowadź hello następujących informacji:

   **Nazwa**: Nazwa hello hello logiki aplikacji.

   **Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.

   **Lokalizacja**: Użyj hello sam lokalizacji, która korzysta z Centrum IoT.
1. Kliknij przycisk **Utwórz**.

### <a name="configure-hello-logic-app"></a>Skonfiguruj aplikację logiki hello

1. Otwórz aplikację logiki hello otwartym w hello projektanta aplikacji logiki.
1. W hello projektanta aplikacji logiki, kliknij przycisk **pustą aplikację logiki**.

   ![Uruchom z aplikacji logiki pusty w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Kliknij przycisk **Service Bus**.

   ![Wybierz opcję tworzenia aplikacji logiki w portalu Azure hello toostart usługi Service Bus](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Kliknij przycisk **usługi Service Bus — nadejściu jedną lub więcej wiadomości w kolejce (automatycznie uzupełniać)**.
1. Utwórz połączenia magistrali usługi.
   1. Wprowadź nazwę połączenia.
   1. Kliknij przestrzeń nazw magistrali usług hello > hello zasad magistrali usługi > **Utwórz**.

      ![Tworzenie połączenia magistrali usługi aplikacji logiki w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Kliknij przycisk **Kontynuuj** po utworzeniu połączenia magistrali usługi hello.
   1. Wybierz kolejki hello, który został utworzony i wprowadź `175` dla **maksymalna liczba komunikatów**

      ![Określ liczbę maksymalną wiadomość hello połączenia magistrali usługi hello w aplikacji logiki](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Kliknij przycisk Zapisz, przycisk toosave hello zmiany.

1. Utwórz połączenie usługi SMTP.
   1. Kliknij przycisk **nowy krok** > **Dodaj akcję**.
   1. Typ `SMTP`, kliknij przycisk hello **SMTP** usług w wyniku wyszukiwania hello, a następnie kliknij przycisk **SMTP — Wyślij wiadomość E-mail**.

      ![Tworzenie połączenia protokołu SMTP w aplikacji logiki w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Wprowadź informacje hello SMTP skrzynki pocztowej, a następnie kliknij przycisk **Utwórz**.

      ![Wprowadź informacje o połączeniu SMTP w aplikacji logiki w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Pobierz informacje hello SMTP dla [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), i [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).
   1. Wprowadź adres e-mail dla **z** i **do**, i `High temperature detected` dla **podmiotu** i **treści**.
   1. Kliknij pozycję **Zapisz**.

Aplikacja logiki Hello jest w stanie podczas zapisywania.

## <a name="test-hello-logic-app"></a>Przetestuj aplikację logiki hello

1. Uruchomić aplikacji klienckiej hello wdrażanego urządzenia tooyour w [tooAzure ESP8266 połączenia Centrum IoT](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Zwiększ temperatury środowiska hello wokół toobe Sensor tag hello powyżej 30 C. Na przykład jasny świecy wokół Twojej Sensor tag.
1. Otrzymasz wiadomość e-mail z powiadomieniem wysyłanych przez aplikację logiki hello.

   > [!NOTE]
   > Usługodawca poczty e-mail może być konieczne jest użytkownik, który wysyła wiadomości e-mail hello toomake tożsamość nadawcy hello tooverify.

## <a name="next-steps"></a>Następne kroki

Pomyślnie utworzono aplikację logiki, która łączy Centrum IoT i skrzynki pocztowej temperatury monitorowania i powiadomień.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
