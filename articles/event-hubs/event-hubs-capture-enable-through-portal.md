---
title: "Włącz aaaAzure przechwytywania centra zdarzeń za pośrednictwem portalu | Dokumentacja firmy Microsoft"
description: "Włącz funkcję przechwytywania centra zdarzeń hello przy użyciu hello portalu Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Włącz przy użyciu portalu Azure hello przechwytywania centra zdarzeń

Można skonfigurować przechwytywania hello zdarzenia koncentratora czas utworzenia przy użyciu hello [portalu Azure](https://portal.azure.com). Można albo przechwytywania tooan danych hello Azure [magazynu obiektów Blob](https://azure.microsoft.com/services/storage/blobs/) kontener lub tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) konta.

## <a name="capture-data-tooan-azure-storage-account"></a>Konto magazynu Azure tooan danych przechwytywania  

Podczas tworzenia Centrum zdarzeń można włączyć przechwytywania, klikając hello **na** przycisku na powitania **tworzenia Centrum zdarzeń** bloku portalu. Następnie możesz określić konto magazynu i kontener, klikając **usługi Azure Storage** w hello **przechwytywania dostawcy** pole. Ponieważ przechwytywania centra zdarzeń korzysta z uwierzytelniania do usługi z magazynem, nie trzeba toospecify parametry połączenia magazynu. Selektor zasobów Hello automatycznie wybiera hello identyfikator URI zasobu dla konta magazynu. Jeśli używasz usługi Azure Resource Manager, musisz jawnie podać ten identyfikator URI jako ciąg.

przedział czasu domyślne Hello jest 5 minut. Hello minimalna wartość to 1, hello maksymalną 15. Witaj **rozmiar** okno ma zakres 10 500 MB.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Konto usługi Azure Data Lake Store tooan danych przechwytywania

toocapture tooAzure danych Data Lake Store, Utwórz konto usługi Data Lake Store i Centrum zdarzeń:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Tworzenie konta i folderów usługi Azure Data Lake Store

1. Utwórz konto usługi Data Lake Store instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Utwórz folder na tym koncie instrukcjami hello w hello [tworzenie folderów w ramach konta usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sekcji.
3. W bloku konta usługi Data Lake Store powitania kliknij **Eksploratora danych**.
4. Kliknij pozycję **Dostęp**.
5. Kliknij pozycję **Dodaj**.
6. W hello **wyszukiwania według nazwy lub e-mail** wpisz **Microsoft.EventHubs** , a następnie wybierz tę opcję. 
7. Witaj **uprawnienia** zostanie wyświetlona karta. Ustaw uprawnienia hello, jak pokazano w następującej ilustracji hello:

    ![][6]

8. Kliknij przycisk **OK**.
9. Teraz Utwórz folder w folderze głównym hello przeglądanie toohello folder docelowy i klikając nazwę folderu hello.
10. Kliknij pozycję **Dostęp**.
11. Kliknij pozycję **Dodaj**.
12. W hello **wyszukiwania według nazwy lub e-mail** wpisz **Microsoft.EventHubs** , a następnie wybierz tę opcję.
13. Witaj **uprawnienia** kartę pojawi się ponownie. Ustaw uprawnienia hello, jak pokazano w następującej ilustracji hello:

    ![][5]

### <a name="create-an-event-hub"></a>Tworzenie centrum zdarzeń

1. Tego Centrum zdarzeń hello musi być w hello tej samej subskrypcji platformy Azure jako hello Azure Data Lake Store właśnie utworzony. Tworzenie Centrum zdarzeń hello, klikając hello **na** przycisku w obszarze **przechwytywania** w hello **tworzenia Centrum zdarzeń** bloku portalu. 
2. W hello **tworzenia Centrum zdarzeń** bloku portalu, wybierz opcję **Azure Data Lake Store** z hello **przechwytywania dostawcy** pole.
3. W **wybierz Data Lake Store**, określ hello utworzonego wcześniej, a w hello konta usługi Data Lake Store **Data Lake ścieżki** wprowadź hello ścieżki toohello folderu danych został utworzony.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Dodawanie lub konfigurowanie funkcji przechwytywania w istniejącym centrum zdarzeń

Przechwytywanie można skonfigurować w istniejących centrach zdarzeń, które znajdują się w przestrzeniach nazw usługi Event Hubs. tooenable przechwytywania na istniejącym Centrum zdarzeń, lub toochange ustawienia przechwytywania, kliknij przycisk hello przestrzeni nazw tooload hello **Essentials** bloku, kliknij przycisk hello Centrum zdarzeń, dla którego chcesz tooenable lub zmienić ustawienie przechwytywania hello. Na koniec kliknij hello **właściwości** sekcji hello otwarcie bloku, a następnie Edytuj ustawienia przechwytywania hello, jak pokazano w hello następujące dane:

### <a name="azure-blob-storage"></a>Azure Blob Storage

![][2]

### <a name="azure-data-lake-store"></a>Azure Data Lake Store

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Następne kroki

Funkcję przechwytywania usługi Event Hubs możesz również skonfigurować za pomocą szablonów usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [Enable Capture using an Azure Resource Manager template (Włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager)](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
