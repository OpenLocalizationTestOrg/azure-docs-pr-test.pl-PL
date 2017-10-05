---
title: "Zapisywania wiadomości Centrum IoT do magazynu danych Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu aplikacji Azure funkcji zapisywania wiadomości Centrum IoT z magazynu tabel Azure. Komunikaty Centrum IoT zawierają informacje, takie jak dane czujników, które są wysyłane z urządzenia IoT."
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
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a>Zapisz komunikaty Centrum IoT, które zawierają dane czujników w celu Twojego magazynu tabel platformy Azure

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Omawiane zagadnienia

Jak utworzyć konto magazynu platformy Azure i aplikacji funkcji platformy Azure do przechowywania komunikatów Centrum IoT w Twoim magazynie w tabeli.

## <a name="what-you-do"></a>Co zrobić

- Utworzenie konta magazynu platformy Azure.
- Przygotuj połączenie Centrum IoT odczytywać wiadomości.
- Tworzenie i wdrażanie aplikacji funkcji platformy Azure.

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

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a>Przygotowanie połączenia Centrum IoT odczytywać wiadomości

Centrum IoT przedstawia punktu końcowego zgodnych z Centrum zdarzeń wbudowanych umożliwia aplikacjom odczytywanie wiadomości Centrum IoT. W tym samym czasie aplikacji umożliwia odczytywanie danych z Centrum IoT grup odbiorców. Przed utworzeniem aplikacji funkcji platformy Azure można odczytać danych z Centrum IoT, wykonaj następujące czynności:

- Pobierz ciąg połączenia punktu końcowego Centrum IoT.
- Utwórz grupy odbiorców Centrum IoT.

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a>Pobierz ciąg połączenia punktu końcowego Centrum IoT

1. Otwórz Centrum IoT.

2. Na **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.

3. W prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.

4. W **właściwości** okienka, należy zwrócić uwagę na następujące wartości:
   - Punkt końcowy zgodnych z Centrum zdarzeń
   - Nazwa zgodnych z Centrum zdarzeń

   ![Pobierz ciąg połączenia punktu końcowego Centrum IoT w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. W **Centrum IoT** okienku w obszarze **ustawienia**, kliknij przycisk **zasady dostępu współużytkowanego**.

6. Kliknij przycisk **iothubowner**.

7. Uwaga **klucz podstawowy** wartość.

8. Utworzenie punktu końcowego Centrum IoT parametry połączenia w następujący sposób:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Zastąp `<Event Hub-compatible endpoint>` i `<Primary key>` wartościami, których wcześniej zapisany.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Tworzenie grupy odbiorców Centrum IoT

1. Otwórz Centrum IoT.

2. W **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.

3. W prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.

4. W **właściwości** okienku w obszarze **grupy konsumentów**, wprowadź nazwę, a następnie zanotuj jego.

5. Kliknij pozycję **Zapisz**.

## <a name="create-and-deploy-an-azure-function-app"></a>Tworzenie i wdrażanie aplikacji Azure — funkcja

1. W [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **obliczeniowe** > **aplikacji funkcji**  >   **Utwórz**.

2. Wprowadź informacje niezbędne do funkcji aplikacji.

   ![Tworzenie aplikacji funkcji w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Nazwa aplikacji**: Nazwa aplikacji funkcji. Nazwa musi być unikatowa w skali globalnej.

   * **Grupa zasobów**: Użyj tej samej grupie zasobów, która używa Centrum IoT.

   * **Konto magazynu**: utworzone konto magazynu.

   * **Przypnij do pulpitu nawigacyjnego**: Zaznacz tę opcję, by mieć łatwy dostęp do aplikacji funkcji z poziomu pulpitu nawigacyjnego.

3. Kliknij przycisk **Utwórz**.

4. Po utworzeniu aplikacji funkcji, można go otworzyć.

5. W funkcji aplikacji Utwórz nową funkcję, wykonując następujące czynności:

   a. Kliknij przycisk **nową funkcję**.

   b. Wybierz **JavaScript** dla **języka**, i **przetwarzania danych** dla **scenariusza**.

   c. Kliknij przycisk **tworzenia tej funkcji**, a następnie kliknij przycisk **nową funkcję**.

   d. Wybierz **JavaScript** dla języka, i **przetwarzania danych** dla tego scenariusza.

   e. Kliknij przycisk **EventHubTrigger JavaScript** szablonu.

   f. Wprowadź informacje niezbędne do szablonu.

      * **Nazwa funkcji**: Nazwa funkcji.

      * **Nazwa Centrum zdarzeń**: Nazwa zgodnych z Centrum zdarzeń zanotowany wcześniej.

      * **Połączenia Centrum zdarzeń**: Aby dodać parametry połączenia utworzonego punktu końcowego Centrum IoT kliknij **nowy**.

   g. Kliknij przycisk **Utwórz**.

6. Dane wyjściowe funkcji należy skonfigurować w następujący sposób:

   a. Kliknij przycisk **integracji** > **nowych danych wyjściowych** > **magazynu tabel Azure** > **wybierz**.

      ![Dodawanie magazynu tabel do funkcji aplikacji w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Wprowadź niezbędne informacje.

      * **Nazwa parametru tabeli**: Użyj `outputTable`, który będzie używany w funkcji platformy Azure kod.
      
      * **Nazwa tabeli**: Użyj `deviceData`.

      * **Konta połączenia z magazynem**: kliknij **nowy**, a następnie wybierz lub wprowadź konta magazynu. Jeśli konto magazynu nie jest wyświetlany, zobacz [wymagania dotyczące konta magazynu](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Kliknij pozycję **Zapisz**.

7. W obszarze **wyzwalaczy**, kliknij przycisk **Azure Event Hub (eventHubMessages)**.

8. W obszarze **grupy odbiorców Centrum zdarzeń**, wprowadź nazwę grupy odbiorców, który zostanie utworzony, a następnie kliknij przycisk **zapisać**.

9. Kliknij funkcję utworzony po lewej stronie, a następnie kliknij przycisk **Wyświetl pliki** po prawej stronie.

10. Zastąp kod w `index.js` następującym kodem:

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. Kliknij pozycję **Zapisz**.

Utworzona aplikacja funkcji. Przechowuje wiadomości, które otrzymuje Centrum IoT w Twoim magazynie w tabeli.

> [!NOTE]
> Można użyć **Uruchom** przycisk, aby przetestować aplikację funkcji. Po kliknięciu **Uruchom**, wiadomości testowej są wysyłane do Centrum IoT. Otrzymanie komunikatu powinno spowodować aplikacji funkcja start, a następnie Zapisz komunikat do magazynu tabel. **Dzienniki** okienko rejestruje szczegółowe informacje o procesie.

## <a name="verify-your-message-in-your-table-storage"></a>Sprawdź wiadomość w Twoim magazynie w tabeli

1. Uruchom przykładową aplikację na urządzeniu do wysyłania komunikatów do Centrum IoT.

2. [Pobieranie i instalowanie Eksploratora usługi Storage Azure](http://storageexplorer.com/).

3. Otwórz Eksploratora usługi Storage, kliknij pozycję **Dodaj konto Azure** > **Zaloguj**, a następnie zaloguj się do konta platformy Azure.

4. Kliknij subskrypcję platformy Azure > **kont magazynu** > Twoje konto magazynu > **tabel** > **deviceData**.

   Powinny pojawić się komunikaty wysyłane z urządzenia do Centrum IoT zalogowany `deviceData` tabeli.

## <a name="next-steps"></a>Następne kroki

Pomyślnie utworzono Twoje konto usługi Azure storage i Azure funkcji aplikacji, która przechowuje komunikaty odbieranych przez Centrum IoT w Twoim magazynie w tabeli.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
