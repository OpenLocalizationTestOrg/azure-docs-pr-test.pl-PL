---
title: "wizualizacji danych czasu aaaReal danych czujnika z Centrum IoT Azure — usługi Power BI | Dokumentacja firmy Microsoft"
description: "Użyj usługi Power BI toovisualize temperatury i wilgotności danych zbieranych z czujnika hello i wysyłane tooyour Centrum Azure IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "wizualizację danych czasu rzeczywistego, wizualizacji danych na żywo czujnik wizualizacji danych"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Wizualizacja danych czujnika w czasie rzeczywistym z Centrum IoT Azure przy użyciu usługi Power BI

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiesz się, jak toovisualize czujnika w czasie rzeczywistym danych Centrum Azure IoT odbieranych przez usługę Power BI. Jeśli chcesz tootry wizualizacji danych hello w Centrum IoT z aplikacjami sieci Web, zobacz [danych czujnika w czasie rzeczywistym toovisualize Użyj Azure Web Apps z Centrum IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Co zrobić

- Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.
- Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia do transferu danych z Twojego tooyour Centrum IoT konta usługi Power BI.
- Tworzenie i publikowanie danych hello toovisualize raportu usługi Power BI.

## <a name="what-you-need"></a>Co jest potrzebne

- Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:
  - Aktywna subskrypcja platformy Azure.
  - Centrum Azure IoT w ramach Twojej subskrypcji.
  - Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.
- Konto usługi Power BI. ([Spróbuj bezpłatnie usługę Power BI](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia

### <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi Stream Analytics

1. W portalu Azure Witaj, kliknij przycisk Nowy > Internetu rzeczy > Zadanie usługi Stream Analytics.
1. Wprowadź następujące informacje dotyczące zadania hello hello.

   **Nazwa zadania**: Nazwa hello hello zadania. Nazwa Hello musi być globalnie unikatowa.

   **Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.

   **Lokalizacja**: Użyj hello sam lokalizacji, w grupie zasobów.

   **Numer PIN toodashboard**: Zaznacz tę opcję, Centrum IoT tooyour łatwy dostęp z poziomu pulpitu nawigacyjnego hello.

   ![Utwórz zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Kliknij przycisk **Utwórz**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Dodaj zadanie usługi analiza strumienia wejściowego toohello

1. Zadanie Stream Analytics hello otwarte.
1. W obszarze **topologii zadania**, kliknij przycisk **dane wejściowe**.
1. W hello **dane wejściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:

   **Alias wejściowy**: hello unikatowego aliasu dla hello danych wejściowych.

   **Źródło**: Wybierz **Centrum IoT**.

   **Grupy odbiorców**: grupy odbiorców hello wybierz właśnie utworzony.
1. Kliknij przycisk **Utwórz**.

   ![Dodaj zadanie usługi analiza strumienia wejściowego tooa na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Dodaj zadanie usługi analiza strumienia wyjściowego toohello

1. W obszarze **topologii zadania**, kliknij przycisk **dane wyjściowe**.
1. W hello **dane wyjściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:

   **Alias wyjściowy**: hello unikatowego aliasu dla hello danych wyjściowych.

   **Obiekt sink**: Wybierz **Power BI**.
1. Kliknij przycisk **autoryzacji**, a następnie zaloguj się na koncie usługi Power BI.
1. Autoryzowany, wprowadź hello następujących informacji:

   **Obszar roboczy grupy**: Wybierz docelowy obszar roboczy grupy.

   **Nazwa zestawu danych**: Wprowadź nazwę zestawu danych.

   **Nazwa tabeli**: Wprowadź nazwę tabeli.
1. Kliknij przycisk **Utwórz**.

   ![Dodaj zadanie usługi analiza strumienia wyjściowego tooa na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Skonfiguruj zapytania hello hello zadania usługi analiza strumienia

1. W obszarze **topologii zadania**, kliknij przycisk **zapytania**.
1. Zastąp `[YourInputAlias]` z aliasem hello wejściowych hello zadania.
1. Zastąp `[YourOutputAlias]` z alias wyjściowy hello hello zadania.
1. Kliknij pozycję **Zapisz**.

   ![Dodaj zadanie usługi Stream Analytics tooa zapytania na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Uruchom zadanie usługi Stream Analytics hello

W zadaniu Stream Analytics hello, kliknij przycisk **Start** > **teraz** > **Start**. Po pomyślnym uruchomieniu zadania hello hello stan zadania zmieni się z **zatrzymane** za**systemem**.

![Uruchom zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Tworzenie i publikowanie danych hello toovisualize raportu usługi Power BI

1. Upewnij się, że hello Przykładowa aplikacja jest uruchomiona na urządzeniu. Jeśli nie mogą odwoływać się samouczki toohello w obszarze [skonfigurować na twoim urządzeniu](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Zaloguj się tooyour [usługi Power BI](https://powerbi.microsoft.com/en-us/) konta.
1. Przejdź toohello obszaru roboczego grupy ustawione podczas tworzenia hello wyjściowego zadania usługi analiza strumienia hello.
1. Kliknij przycisk **przesyłania strumieniowego zestawów danych**.

   Zestaw danych hello wymienione określony podczas tworzenia hello dane wyjściowe zadania usługi analiza strumienia hello powinna zostać wyświetlona.
1. W obszarze **akcje**, kliknij pierwszy hello toocreate ikonę raportu.

   ![Tworzenie raportu usługi Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Tworzenie linii temperatury w czasie rzeczywistym tooshow wykresu wraz z upływem czasu.
   1. Na stronie tworzenia raportu hello Dodaj wykres liniowy.
   1. Na powitania **pola** okienku rozwiń tabeli hello określone podczas tworzenia hello wyjściowego zadania usługi analiza strumienia hello.
   1. Przeciągnij **EventEnqueuedUtcTime** za**osi** na powitania **wizualizacje** okienka.
   1. Przeciągnij **temperatury** za**wartości**.

      Teraz jest tworzony wykres liniowy. oś x Hello Wyświetla datę i godzinę w strefie czasowej UTC hello. oś y Hello Wyświetla temperatury z czujnika hello.

      ![Dodaj wykres liniowy dla tooa temperatury raportu usługi Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Utwórz innego wiersza wykresu tooshow w czasie rzeczywistym wilgotności wraz z upływem czasu. toodo, wykonaj hello same kroki opisane powyżej i umieścić **EventEnqueuedUtcTime** na osi x hello i **wilgotności** na powitania osi y.

   ![Dodaj wykres wiersza wilgotność tooa raportu usługi Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Kliknij przycisk **zapisać** toosave hello raportu.
1. Kliknij przycisk **pliku** > **publikowania tooweb**.
1. Kliknij przycisk **kod osadzania, Utwórz**, a następnie kliknij przycisk **publikowania**.

W przypadku podane łącze do raportu hello, które można udostępniać każda osoba, aby uzyskać dostęp do raportów i raportu hello toointegrate fragment kodu w blogu lub witrynie sieci Web.

![Publikowanie raportu Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Firma Microsoft oferuje również hello [aplikacji mobilnych usługi Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) do przeglądania i interakcji z raportów i pulpitów nawigacyjnych usługi Power BI na swoim urządzeniu przenośnym.

## <a name="next-steps"></a>Następne kroki

Pomyślnie zastosowano danych czujnika w czasie rzeczywistym toovisualize usługi Power BI z Centrum Azure IoT.
Brak danych toovisualize alternatywny sposób z Centrum IoT Azure. Zobacz [danych czujnika w czasie rzeczywistym toovisualize Użyj Azure Web Apps z Centrum IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
