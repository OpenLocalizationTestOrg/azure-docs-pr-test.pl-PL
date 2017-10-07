---
title: "aaaSave Centrum IoT wiadomości magazynu danych tooAzure | Dokumentacja firmy Microsoft"
description: "Użyj toosave aplikacji Azure — funkcja Twoje tooyour wiadomości Centrum IoT magazynu tabel platformy Azure. wiadomości powitania od centrum IoT zawierają informacje, takie jak dane czujników, które są wysyłane z urządzenia IoT."
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
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Zapisz komunikaty Centrum IoT, które zawierają magazynu tabel Azure tooyour danych czujnika

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiedz się, jak komunikaty Centrum IoT toostore aplikacji w Twoim magazynie w tabeli funkcji toocreate konta magazynu platformy Azure i platformy Azure.

## <a name="what-you-do"></a>Co zrobić

- Utworzenie konta magazynu platformy Azure.
- Przygotuj Centrum IoT połączenia tooread wiadomości.
- Tworzenie i wdrażanie aplikacji funkcji platformy Azure.

## <a name="what-you-need"></a>Co jest potrzebne

- [Urządzenie jest skonfigurowane](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover następujące wymagania:
  - Aktywną subskrypcją platformy Azure
  - Centrum IoT w ramach Twojej subskrypcji 
  - Uruchomionych aplikacji, która wysyła Centrum IoT tooyour wiadomości

## <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage

1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **magazynu** > **konta magazynu**  >   **Utwórz**.

2. Wprowadź niezbędne informacje powitania dla konta magazynu hello:

   ![Utwórz konto magazynu w hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Nazwa**: Nazwa hello hello konta magazynu. Nazwa Hello musi być globalnie unikatowa.

   * **Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.

   * **Numer PIN toodashboard**: Wybierz tę opcję, Centrum IoT tooyour łatwy dostęp z hello pulpitu nawigacyjnego.

3. Kliknij przycisk **Utwórz**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Przygotowanie Centrum IoT komunikaty tooread połączenia.

Centrum IoT udostępnia wbudowane punktu końcowego Centrum zgodnego tooenable aplikacji tooread IoT Centrum komunikaty o zdarzeniach. W tym samym czasie aplikacje używają danych tooread grupy konsumentów z Centrum IoT. Przed utworzeniem tooread dane aplikacji Azure funkcji z Centrum IoT hello następujące:

- Pobierz ciąg połączenia hello punktu końcowego Centrum IoT.
- Utwórz grupy odbiorców Centrum IoT.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>Pobierz ciąg połączenia hello punktu końcowego Centrum IoT

1. Otwórz Centrum IoT.

2. Na powitania **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.

3. W hello prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.

4. W hello **właściwości** okienka, hello Uwaga następujące wartości:
   - Punkt końcowy zgodnych z Centrum zdarzeń
   - Nazwa zgodnych z Centrum zdarzeń

   ![Pobierz ciąg połączenia hello punktu końcowego Centrum IoT w hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. W hello **Centrum IoT** okienku w obszarze **ustawienia**, kliknij przycisk **zasady dostępu współużytkowanego**.

6. Kliknij przycisk **iothubowner**.

7. Uwaga hello **klucz podstawowy** wartość.

8. Utwórz hello parametry połączenia punktu końcowego Centrum IoT w następujący sposób:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Zastąp `<Event Hub-compatible endpoint>` i `<Primary key>` wartościami hello zanotowany wcześniej.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Tworzenie grupy odbiorców Centrum IoT

1. Otwórz Centrum IoT.

2. W hello **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.

3. W hello prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.

4. W hello **właściwości** okienku w obszarze **grupy konsumentów**, wprowadź nazwę, a następnie zanotuj jego.

5. Kliknij pozycję **Zapisz**.

## <a name="create-and-deploy-an-azure-function-app"></a>Tworzenie i wdrażanie aplikacji Azure — funkcja

1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **obliczeniowe** > **aplikacji funkcji**  >   **Utwórz**.

2. Wprowadź niezbędne informacje hello hello funkcji aplikacji.

   ![Tworzenie aplikacji funkcji w hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Nazwa aplikacji**: Nazwa hello hello funkcji aplikacji. Nazwa Hello musi być globalnie unikatowa.

   * **Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.

   * **Konto magazynu**: hello utworzone konto magazynu.

   * **Numer PIN toodashboard**: Zaznacz tę opcję dla aplikacji funkcja toohello łatwy dostęp z poziomu pulpitu nawigacyjnego hello.

3. Kliknij przycisk **Utwórz**.

4. Po utworzeniu hello funkcji aplikacji, można go otworzyć.

5. W aplikacji funkcji hello Utwórz nową funkcję, wykonując następujące hello:

   a. Kliknij przycisk **nową funkcję**.

   b. Wybierz **JavaScript** dla **języka**, i **przetwarzania danych** dla **scenariusza**.

   c. Kliknij przycisk **tworzenia tej funkcji**, a następnie kliknij przycisk **nową funkcję**.

   d. Wybierz **JavaScript** dla języka hello i **przetwarzania danych** hello scenariusza.

   e. Kliknij przycisk hello **EventHubTrigger JavaScript** szablonu.

   f. Wprowadź niezbędne informacje hello hello szablonu.

      * **Nazwa funkcji**: Nazwa hello hello funkcji.

      * **Nazwa Centrum zdarzeń**: Nazwa zgodnych z Centrum zdarzeń hello zanotowany wcześniej.

      * **Połączenia Centrum zdarzeń**: parametry połączenia hello tooadd hello punktu końcowego Centrum IoT utworzony, kliknij przycisk **nowy**.

   g. Kliknij przycisk **Utwórz**.

6. Skonfiguruj wyjścia funkcji hello, wykonując następujące hello:

   a. Kliknij przycisk **integracji** > **nowych danych wyjściowych** > **magazynu tabel Azure** > **wybierz**.

      ![Dodatek tabeli magazynu tooyour funkcji aplikacji hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Wprowadź niezbędne informacje hello.

      * **Nazwa parametru tabeli**: Użyj `outputTable`, który będzie używany w hello Azure kodu funkcji.
      
      * **Nazwa tabeli**: Użyj `deviceData`.

      * **Konta połączenia z magazynem**: kliknij **nowy**, a następnie wybierz lub wprowadź konta magazynu. Jeśli konto magazynu hello nie jest wyświetlany, zobacz [wymagania dotyczące konta magazynu](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Kliknij pozycję **Zapisz**.

7. W obszarze **wyzwalaczy**, kliknij przycisk **Azure Event Hub (eventHubMessages)**.

8. W obszarze **grupy odbiorców Centrum zdarzeń**, wprowadź nazwę grupy odbiorców hello utworzone, a następnie kliknij przycisk hello **zapisać**.

9. Kliknij przycisk Funkcja powitania po utworzeniu na powitania po lewej, a następnie kliknij przycisk **Wyświetl pliki** na powitania prawo.

10. Zastąp kod hello w `index.js` hello następujący:

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
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

Utworzona hello funkcji aplikacji. Przechowuje wiadomości, które otrzymuje Centrum IoT w Twoim magazynie w tabeli.

> [!NOTE]
> Można użyć hello **Uruchom** przycisk tootest hello funkcji aplikacji. Po kliknięciu **Uruchom**, tooyour Centrum IoT jest wysłać wiadomości testowej hello. Hello nadejście wiadomości powitania powinien wyzwolenia hello funkcji aplikacji toostart, a następnie zapisz magazynu tabel tooyour wiadomość hello. Witaj **dzienniki** okienko rejestruje szczegóły hello hello procesu.

## <a name="verify-your-message-in-your-table-storage"></a>Sprawdź wiadomość w Twoim magazynie w tabeli

1. Uruchom hello przykładowej aplikacji w Centrum IoT tooyour wiadomości toosend urządzenia.

2. [Pobieranie i instalowanie Eksploratora usługi Storage Azure](http://storageexplorer.com/).

3. Otwórz Eksploratora usługi Storage, kliknij pozycję **Dodaj konto usługi Azure** > **Zaloguj**, a następnie zaloguj tooyour konto platformy Azure.

4. Kliknij subskrypcję platformy Azure > **kont magazynu** > Twoje konto magazynu > **tabel** > **deviceData**.

   Powinny pojawić się komunikaty wysyłane z Centrum IoT tooyour urządzenia zarejestrowane w hello `deviceData` tabeli.

## <a name="next-steps"></a>Następne kroki

Pomyślnie utworzono Twoje konto usługi Azure storage i Azure funkcji aplikacji, która przechowuje komunikaty odbieranych przez Centrum IoT w Twoim magazynie w tabeli.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
