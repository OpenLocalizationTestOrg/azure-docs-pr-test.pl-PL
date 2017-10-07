---
title: "aaaCapture danych z usługi Event Hubs do usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Data Lake Store toocapture danych z usługi Event Hubs"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Użyj usługi Azure Data Lake Store toocapture danych z usługi Event Hubs

Dowiedz się, jak toouse Azure Data Lake Store toocapture danych odebranych przez usługi Azure Event Hubs.

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md).

*  **Centra zdarzeń w przestrzeni nazw**. Aby uzyskać instrukcje, zobacz [tworzenie przestrzeni nazw usługi Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Upewnij się, że konto usługi Data Lake Store hello i przestrzeni nazw usługi Event Hubs hello znajdują się w hello tej samej subskrypcji platformy Azure.


## <a name="assign-permissions-tooevent-hubs"></a>Przypisz uprawnienia tooEvent koncentratory

W tej sekcji należy utworzyć folder w ramach konta hello miejscu toocapture hello dane z usługi Event Hubs. Można także przypisać uprawnienia koncentratory tooEvent tak, aby ją zapisać danych do konta usługi Data Lake Store. 

1. Otwieranie konta usługi Data Lake Store hello gdzie toocapture dane z usługi Event Hubs, a następnie kliknij polecenie **Eksploratora danych**.

    ![Eksplorator danych Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Eksploratora danych usługi Data Lake Store")

2.  Kliknij przycisk **nowy Folder** , a następnie wprowadź nazwę folderu, w którym ma toocapture hello danych.

    ![Utwórz nowy folder w usłudze Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Utwórz nowy folder w usłudze Data Lake Store")

3. Przypisz uprawnienia w katalogu głównym hello hello usługi Data Lake Store. 

    a. Kliknij przycisk **Eksploratora danych**wybierz katalog główny hello hello konta usługi Data Lake Store, a następnie kliknij przycisk **dostępu**.

    ![Przypisywanie uprawnień do katalogu głównego usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "przypisać uprawnienia dla elementu głównego usługi Data Lake Store")

    b. W obszarze **dostępu**, kliknij przycisk **Dodaj**, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie wyszukaj `Microsoft.EventHubs`. 

    ![Przypisywanie uprawnień do katalogu głównego usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "przypisać uprawnienia dla elementu głównego usługi Data Lake Store")
    
    Kliknij pozycję **Wybierz**.

    c. W obszarze **przypisywanie uprawnień**, kliknij przycisk **wybierz uprawnienia**. Ustaw **uprawnienia** za**Execute**. Ustaw **dodać do** za**ten folder i wszystkie obiekty podrzędne**. Ustaw **dodać jako** za**wpisu uprawnienia dostępu i wpis uprawnienia domyślne**.

    ![Przypisywanie uprawnień do katalogu głównego usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "przypisać uprawnienia dla elementu głównego usługi Data Lake Store")

    Kliknij przycisk **OK**.

4. Przypisanie uprawnień dla folderu hello w ramach konta usługi Data Lake Store, w którym ma toocapture danych.

    a. Kliknij przycisk **Eksploratora danych**, wybierz hello folder hello konta usługi Data Lake Store, a następnie kliknij przycisk **dostępu**.

    ![Przypisanie uprawnień dla folderu usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "przypisanie uprawnień dla folderu usługi Data Lake Store")

    b. W obszarze **dostępu**, kliknij przycisk **Dodaj**, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie wyszukaj `Microsoft.EventHubs`. 

    ![Przypisanie uprawnień dla folderu usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "przypisanie uprawnień dla folderu usługi Data Lake Store")
    
    Kliknij pozycję **Wybierz**.

    c. W obszarze **przypisywanie uprawnień**, kliknij przycisk **wybierz uprawnienia**. Ustaw **uprawnienia** za**Odczyt, zapis,** i **Execute**. Ustaw **dodać do** za**ten folder i wszystkie obiekty podrzędne**. Wreszcie, ustaw **dodać jako** za**wpisu uprawnienia dostępu i wpis uprawnienia domyślne**.

    ![Przypisanie uprawnień dla folderu usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "przypisanie uprawnień dla folderu usługi Data Lake Store")
    
    Kliknij przycisk **OK**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Konfigurowanie usługi Event Hubs toocapture tooData usługi data Lake Store

W tej sekcji utworzysz Centrum zdarzeń w przestrzeni nazw usługi Event Hubs. Możesz również skonfigurować hello Centrum zdarzeń toocapture danych tooan konta usługi Azure Data Lake Store. W tej sekcji założono, że utworzono już przestrzeń nazw usługi Event Hubs.

2. Z hello **omówienie** kliknij okienko hello przestrzeni nazw usługi Event Hubs, **+ Centrum zdarzeń**.

    ![Tworzenie Centrum zdarzeń](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "tworzenia Centrum zdarzeń")

3. Podaj poniżej hello wartości tooconfigure usługi Event Hubs toocapture danych tooData Lake Store.

    ![Tworzenie Centrum zdarzeń](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "tworzenia Centrum zdarzeń")

    a. Podaj nazwę hello Centrum zdarzeń.
    
    b. W tym samouczku, ustaw **liczba partycji** i **przechowywania wiadomości** toohello wartości domyślne.
    
    c. Ustaw **przechwytywania** za**na**. Zestaw hello **przedział czasu** (częstotliwość toocapture) i **rozmiar okna** (toocapture rozmiar danych). 
    
    d. Dla **przechwytywania dostawcy**, wybierz pozycję **Azure Data Lake Store** i hello wybierz hello utworzoną wcześniej usługi Data Lake Store. Dla **Data Lake ścieżka**, wprowadź nazwę hello hello folderu utworzonego w hello konta usługi Data Lake Store. Wystarczy tooprovide hello ścieżki względnej toohello folderu.

    e. Pozostaw hello **formatów nazwy pliku przechwytywania próbki** toohello wartości domyślnej. Ta opcja reguluje hello struktury folderów, który jest tworzony w folderze przechwytywania hello.

    f. Kliknij przycisk **Utwórz**.

## <a name="test-hello-setup"></a>Instalator hello testu

Teraz możesz przetestować rozwiązania hello wysyłając toohello danych Azure Event Hub. Postępuj zgodnie z instrukcjami hello w [wysyłać zdarzenia tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Po uruchomieniu wysyłanie danych hello, zostaną wyświetlone hello dane zostaną uwzględnione w usłudze Data Lake Store za pomocą struktury folderów hello określona. Na przykład zostanie wyświetlony strukturę folderów, jak pokazano w hello następującego zrzutu ekranu w usługi Data Lake Store.

![Przykładowe dane EventHub w usłudze Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "EventHub przykładowych danych w usłudze Data Lake Store")

> [!NOTE]
> Nawet jeśli nie masz wiadomości przychodzących do usługi Event Hubs, usługa Event Hubs zapisuje pustych plików z tylko nagłówki hello do hello konta usługi Data Lake Store. Witaj pliki są zapisywane na powitania sam podanemu podczas tworzenia usługi Event Hubs hello interwał czasu.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Analizowanie danych w usłudze Data Lake Store

Po hello danych w usłudze Data Lake Store można uruchamiać zadania analityczne dane hello tooprocess i wykonywać. Zobacz [USQL Avro przykład](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) na temat toodo to przy użyciu usługi Azure Data Lake Analytics.
  

## <a name="see-also"></a>Zobacz też
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
