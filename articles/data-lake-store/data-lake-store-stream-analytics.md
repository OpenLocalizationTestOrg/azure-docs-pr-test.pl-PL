---
title: "aaaStream danych z usługi Stream Analytics do usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Stream Analytics toostream danych do usługi Azure Data Lake Store"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics (Strumieniowe przesyłanie danych z obiektu blob usługi Azure Storage do usługi Data Lake Store za pomocą usługi Azure Stream Analytics)
W tym artykule dowiesz się, jak toouse Azure Data Lake przechowywać jako dane wyjściowe zadania usługi analiza strumienia Azure. W tym artykule przedstawiono prosty scenariusz służącą do odczytywania danych z obiektu blob magazynu Azure (dane wejściowe), a następnie zapisuje hello danych tooData Lake Store (dane wyjściowe).

> [!NOTE]
> W tej chwili tworzenia i konfigurowania usługi Data Lake Store generuje Stream Analytics jest obsługiwane tylko w hello [klasycznego portalu Azure](https://manage.windowsazure.com). W związku z tym niektórych części tego samouczka zostanie użyty hello klasycznego portalu Azure.
>
>

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Konto usługi Azure Storage**. Zadanie Stream Analytics będzie używać kontenera obiektów blob z konta tooinput danych. W tym samouczku założono, że masz konto magazynu o nazwie **storageforasa** i wywołać kontenera w ramach konta hello **storageforasacontainer**. Po utworzeniu kontenera hello, Przekaż przykładowe dane pliku tooit. 
  
* **Konto usługi Azure Data Lake Store**. Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md). Załóżmy, że masz konto usługi Data Lake Store o nazwie **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi analiza strumienia
Rozpoczyna się od utworzenia zadanie usługi Stream Analytics, która zawiera źródło danych wejściowych i miejsce docelowe danych wyjściowych. W tym samouczku hello źródła jest kontenera obiektów blob platformy Azure i miejsce docelowe hello jest Data Lake Store.

1. Zaloguj się na toohello [Azure Portal](https://portal.azure.com).

2. W okienku po lewej stronie powitania kliknij **zadania usługi analiza strumienia**, a następnie kliknij przycisk **Dodaj**.

    ![Tworzenie zadania usługi analiza strumienia](./media/data-lake-store-stream-analytics/create.job.png "utworzyć zadania usługi analiza strumienia")

    > [!NOTE]
    > Upewnij się, że zadania tworzenia w hello tym samym regionie co konto magazynu hello lub spowoduje naliczenie dodatkowych kosztów przenoszenia danych między regionami.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Tworzenie obiektu Blob danych wejściowych hello zadania

1. Otwórz hello hello zadania usługi analiza strumienia, w okienku po lewej stronie powitania kliknij hello **dane wejściowe** , a następnie kliknij pozycję **Dodaj**.

    ![Dodaj zadanie wejściowych tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "dodać zadania tooyour wejściowych")

2. Na powitania **wprowadzania nowych** bloku, podaj następujące wartości hello.

    ![Dodaj zadanie wejściowych tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "dodać zadania tooyour wejściowych")

    * Dla **alias wejściowy**, wprowadź unikatową nazwę dla zadania hello w danych wejściowych.
    * Aby uzyskać **typ źródła**, wybierz pozycję **strumienia danych**.
    * Aby uzyskać **źródła**, wybierz pozycję **magazynu obiektów Blob**.
    * Aby uzyskać **subskrypcji**, wybierz pozycję **Użyj magazynu obiektów blob z bieżącej subskrypcji**.
    * Aby uzyskać **konta magazynu**, wybierz konto magazynu hello, utworzony jako część hello wymagania wstępne. 
    * Dla **kontenera**, wybierz kontener hello, który został utworzony w hello wybranego konta magazynu.
    * Aby uzyskać **format serializacji zdarzeń**, wybierz pozycję **CSV**.
    * Aby uzyskać **ogranicznik**, wybierz pozycję **kartę**.
    * Aby uzyskać **kodowanie**, wybierz pozycję **UTF-8**.

    Kliknij przycisk **Utwórz**. Hello portal teraz dodaje dane wejściowe hello i testy hello tooit połączenia.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Utwórz dane wyjściowe zadania hello usługi Data Lake Store

1. Otwórz stronę hello zadania usługi analiza strumienia hello, kliknij przycisk hello **dane wyjściowe** , a następnie kliknij pozycję **Dodaj**.

    ![Dodawanie danych wyjściowych zadania tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "dodać zadania tooyour danych wyjściowych")

2. Na powitania **nowe dane wyjściowe** bloku, podaj następujące wartości hello.

    ![Dodawanie danych wyjściowych zadania tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "dodać zadania tooyour danych wyjściowych")

    * Dla **alias wyjściowy**, wprowadź unikatową nazwę hello dane wyjściowe zadania. Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis usługi Data Lake Store.
    * Aby uzyskać **Sink**, wybierz pozycję **usługi Data Lake Store**.
    * Zostanie wyświetlony monit o tooauthorize będzie można uzyskać dostęp do konta tooData Lake Store. Kliknij przycisk **autoryzować**.

3. Na powitania **nowe dane wyjściowe** bloku kontynuować hello tooprovide następujące wartości.

    ![Dodawanie danych wyjściowych zadania tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "dodać zadania tooyour danych wyjściowych")

    * Aby uzyskać **nazwa konta**, wybierz konto usługi Data Lake Store hello utworzone miejsce toobe dane wyjściowe zadania hello wysyłane do.
    * Dla **wzorzec prefiksu ścieżki**, wprowadź toowrite użyta ścieżka pliku pliki w obrębie hello określone konto usługi Data Lake Store.
    * Aby uzyskać **format daty**, jeśli token daty jest używany w ścieżce prefiks hello, można wybrać format daty hello, w którym pliki są organizowane.
    * Dla **format czasu**, jeśli token czasu używany w ścieżce prefiks hello, określ hello format czasu, w którym pliki są organizowane.
    * Aby uzyskać **format serializacji zdarzeń**, wybierz pozycję **CSV**.
    * Aby uzyskać **ogranicznik**, wybierz pozycję **kartę**.
    * Aby uzyskać **kodowanie**, wybierz pozycję **UTF-8**.
    
    Kliknij przycisk **Utwórz**. Hello portal teraz dodaje dane wyjściowe hello i testy hello tooit połączenia.
    
## <a name="run-hello-stream-analytics-job"></a>Uruchom zadanie usługi Stream Analytics hello

1. toorun zadanie usługi Stream Analytics, należy uruchomić zapytania z hello **zapytania** kartę. W tym samouczku, można uruchomić hello przykładowe zapytanie, zastępując symbole zastępcze hello z hello zadania wejściowymi i wyjściowymi aliasy, jak pokazano w poniższym zrzucie ekranu hello.

    ![Uruchom zapytanie](./media/data-lake-store-stream-analytics/run.query.png ", uruchom zapytanie")

2. Kliknij przycisk **zapisać** od góry hello hello ekranu, a następnie z hello **omówienie** , kliknij pozycję **Start**. W oknie dialogowym hello, wybierz **czasu niestandardowe**, a następnie ustaw hello bieżącą datę i godzinę.

    ![Ustawianie czasu zadania](./media/data-lake-store-stream-analytics/run.query.2.png "ustawić czas pracy")

    Kliknij przycisk **Start** toostart hello zadania. Może potrwać tooa kilka minut toostart hello zadania.

3. tootrigger hello zadania toopick hello danych z obiektu blob hello, skopiuj kontenera obiektów blob toohello plików przykładowych danych. Możesz pobrać przykładowy plik danych ze hello [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). W tym samouczku, skopiuj plik hello **vehicle1_09142014.csv**. Można użyć różnych klientów, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/), tooupload danych tooa obiektów blob kontenera.

4. Z hello **omówienie** , w obszarze **monitorowanie**, zobacz przetwarzaniu hello danych.

    ![Zadanie monitora](./media/data-lake-store-stream-analytics/run.query.3.png "zadania monitora")

5. Na koniec można sprawdzić, czy dane wyjściowe zadania hello jest dostępna w hello konta usługi Data Lake Store. 

    ![Sprawdź dane wyjściowe](./media/data-lake-store-stream-analytics/run.query.4.png "Sprawdź dane wyjściowe")

    W okienku Eksplorator danych hello, zwróć uwagę, że hello output, ścieżka folderu tooa zapisywane jako określono w hello ustawienia danych wyjściowych usługi Data Lake Store (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Zobacz też
* [Utwórz toouse klastra usługi HDInsight usługi Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
