---
title: "Zapisywania wiadomości Centrum IoT do magazynu danych Azure | Dokumentacja firmy Microsoft"
description: "Użyj Centrum IoT rozsyłania wiadomości do zapisywania wiadomości Centrum IoT do usługi magazynu obiektów blob platformy Azure. Komunikaty Centrum IoT zawierają informacje, takie jak dane czujników, które są wysyłane z urządzenia IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Magazyn danych iot, przechowywania danych czujników iot"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/04/2017
ms.author: xshi
ms.openlocfilehash: 5419f0fb86f2a7b051ffc7fda17c74cf15178a6b
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-blob-storage"></a>Zapisz komunikaty Centrum IoT, które zawierają dane czujników do usługi magazynu obiektów blob platformy Azure

![Diagram end-to-end](media/iot-hub-store-data-in-azure-table-storage/1_route-to-storage.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Omawiane zagadnienia

Jak utworzyć konto magazynu platformy Azure i aplikacji funkcji platformy Azure do przechowywania wiadomości Centrum IoT w magazynie obiektów blob.

## <a name="what-you-do"></a>Co zrobić

- Utworzenie konta magazynu platformy Azure.
- Przygotuj Centrum IoT do przesyłania wiadomości do magazynu.

## <a name="what-you-need"></a>Co jest potrzebne

- [Urządzenie jest skonfigurowane](iot-hub-raspberry-pi-kit-node-get-started.md) , aby pokrywał się następujące wymagania:
  - Aktywną subskrypcją platformy Azure
  - Centrum IoT w ramach Twojej subskrypcji 
  - Działającej aplikacji, która wysyła komunikaty do Centrum IoT

## <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage

1. W [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **magazynu** > **konta magazynu**  >   **Utwórz**.

2. Wprowadź informacje niezbędne do konta magazynu:

   ![Utwórz konto magazynu w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Nazwa**: Nazwa konta magazynu. Nazwa musi być unikatowa w skali globalnej.

   * **Grupa zasobów**: Użyj tej samej grupie zasobów, która używa Centrum IoT.

   * **Przypnij do pulpitu nawigacyjnego**: wybierz tę opcję, aby mieć łatwy dostęp do centrum IoT Hub z pulpitu nawigacyjnego.

3. Kliknij przycisk **Utwórz**.

## <a name="prepare-your-iot-hub-to-route-messages-to-storage"></a>Przygotowanie do wyznaczania tras wiadomościom magazynu Centrum IoT

Centrum IoT natywnie obsługuje rozesłania wiadomości do magazynu Azure jako obiekty BLOB.

### <a name="add-storage-as-a-custom-endpoint"></a>Dodawanie magazynu jako punktu końcowego niestandardowych

Przejdź do Centrum IoT w portalu Azure. Kliknij przycisk **punkty końcowe** > **dodać**. Nazwa punktu końcowego, a następnie wybierz **kontenera magazynu Azure** jako typ punktu końcowego. Użyj selektora, aby wybrać konto magazynu, który został utworzony w poprzedniej sekcji. Utworzyć kontenera magazynu i wybierz go, a następnie kliknij przycisk **OK**.

  ![Tworzenie punktu końcowego niestandardowych w Centrum IoT](media\iot-hub-store-data-in-azure-table-storage\2_custom-storage-endpoint.png)

### <a name="add-a-route-to-route-data-to-storage"></a>Dodaj dane trasy do trasy do magazynu

Kliknij przycisk **tras** > **Dodaj** i wprowadź nazwę dla trasy. Wybierz **komunikaty** jako źródło danych i wybierz punktu końcowego magazynu właśnie utworzony jako punkt końcowy w trasie. Wprowadź `true` jako ciąg zapytania, następnie kliknij przycisk **zapisać**.

  ![Utwórz trasę w Centrum IoT](media\iot-hub-store-data-in-azure-table-storage\3_create-route.png)
  
### <a name="add-a-route-for-hot-path-telemetry-optional"></a>Dodaj trasę dla danych telemetrycznych aktywnej ścieżki (opcjonalnie)

Domyślnie Centrum IoT kieruje wszystkie komunikaty, które nie są zgodne z innymi trasy do punktu końcowego wbudowanych. Ponieważ wszystkie komunikaty o telemetrii teraz zgodne z regułą, który kieruje komunikaty do magazynu, musisz dodać innej trasy dla komunikatów do zapisania wbudowanym punktem końcowym. Brak bez dodatkowych opłat do wyznaczania tras wiadomościom wiele punktów końcowych.

> [!NOTE]
> Ten krok można pominąć, jeśli nie przeprowadzasz dodatkowe przetwarzanie komunikatów o telemetrii.

Kliknij przycisk **Dodaj** z okienka tras i wprowadź nazwę dla trasy. Wybierz **komunikaty** jako źródło danych i **zdarzenia** jako punkt końcowy. Wprowadź `true` jako ciąg zapytania, następnie kliknij przycisk **zapisać**.

  ![Utwórz trasę ścieżki hot w Centrum IoT](media\iot-hub-store-data-in-azure-table-storage\4_hot-path-route.png)

## <a name="verify-your-message-in-your-storage-container"></a>Sprawdź wiadomość w kontenerze z magazynu

1. Uruchom przykładową aplikację na urządzeniu do wysyłania komunikatów do Centrum IoT.

2. [Pobieranie i instalowanie Eksploratora usługi Storage Azure](http://storageexplorer.com/).

3. Otwórz Eksploratora usługi Storage, kliknij pozycję **Dodaj konto Azure** > **Zaloguj**, a następnie zaloguj się do konta platformy Azure.

4. Kliknij subskrypcję platformy Azure > **kont magazynu** > Twoje konto magazynu > **kontenerów obiektów Blob** > z kontenera.

   Powinny pojawić się komunikaty wysyłane z urządzenia do Centrum IoT rejestrowane w kontenerze obiektów blob.

## <a name="next-steps"></a>Następne kroki

Utworzono pomyślnie Twoje konto magazynu Azure i routingiem wiadomości z Centrum IoT do kontenera obiektów blob na tym koncie magazynu.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
