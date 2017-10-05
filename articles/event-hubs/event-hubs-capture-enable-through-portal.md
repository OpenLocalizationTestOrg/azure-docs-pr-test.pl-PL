---
title: "Włączanie funkcji przechwytywania usługi Azure Event Hubs przy użyciu portalu | Microsoft Docs"
description: "Włącz funkcję przechwytywania usługi Event Hubs przy użyciu witryny Azure Portal."
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a>Włączanie funkcji przechwytywania usługi Event Hubs przy użyciu witryny Azure Portal

Przy użyciu witryny [Azure Portal](https://portal.azure.com) można skonfigurować funkcję przechwytywania podczas tworzenia centrum zdarzeń. Dane mogą być przechwytywane do kontenera usługi Azure [Blob Storage](https://azure.microsoft.com/services/storage/blobs/) lub na konto usługi [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

## <a name="capture-data-to-an-azure-storage-account"></a>Przechwytywanie danych na konto usługi Azure Storage  

Podczas tworzenia Centrum zdarzeń można włączyć przechwytywania, klikając **na** przycisk **tworzenia Centrum zdarzeń** bloku portalu. Następnie można określić konto magazynu i kontener przez kliknięcie pozycji **Azure Storage** w polu **Dostawca przechwytywania**. Ponieważ do uwierzytelniania w magazynie funkcja przechwytywania usługi Event Hubs korzysta z uwierzytelniania między usługami, nie trzeba podawać parametrów połączenia z magazynem. Selektor zasobów automatycznie wybiera identyfikator URI zasobu dla konta magazynu. Jeśli używasz usługi Azure Resource Manager, musisz jawnie podać ten identyfikator URI jako ciąg.

Domyślny przedział czasu to 5 minut. Minimalna wartość to 1, a maksymalna — 15. Okno **Rozmiar** ma zakres 10–500 MB.

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a>Przechwytywanie danych na konto usługi Azure Data Lake Store

Aby przechwycić dane do usługi Azure Data Lake Store, należy utworzyć konto usługi Data Lake Store i centrum zdarzeń:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Tworzenie konta i folderów usługi Azure Data Lake Store

1. Utwórz konto usługi Data Lake Store, postępując zgodnie z instrukcjami w temacie [Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą witryny Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Utwórz folder na tym koncie, postępując zgodnie z instrukcjami w sekcji [Tworzenie folderów w ramach konta usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).
3. W bloku konta usługi Data Lake Store, kliknij **Eksploratora danych**.
4. Kliknij pozycję **Dostęp**.
5. Kliknij pozycję **Dodaj**.
6. W polu **Wyszukaj według nazwy lub adresu e-mail** wpisz **Microsoft.EventHubs**, a następnie wybierz tę opcję. 
7. Zostanie wyświetlona karta **Uprawnienia**. Ustaw uprawnienia, jak pokazano na poniższej ilustracji:

    ![][6]

8. Kliknij przycisk **OK**.
9. Następnie utwórz folder w folderze głównym przez przejście do folderu docelowego i kliknięcie nazwy folderu.
10. Kliknij pozycję **Dostęp**.
11. Kliknij pozycję **Dodaj**.
12. W polu **Wyszukaj według nazwy lub adresu e-mail** wpisz **Microsoft.EventHubs**, a następnie wybierz tę opcję.
13. Ponownie zostanie wyświetlona karta **Uprawnienia**. Ustaw uprawnienia, jak pokazano na poniższej ilustracji:

    ![][5]

### <a name="create-an-event-hub"></a>Tworzenie centrum zdarzeń

1. Centrum zdarzeń musi należeć do tej samej subskrypcji platformy Azure co właśnie utworzone konto usługi Azure Data Lake Store. Tworzenie Centrum zdarzeń, klikając pozycję **na** przycisku w obszarze **przechwytywania** w **tworzenia Centrum zdarzeń** bloku portalu. 
2. W **tworzenia Centrum zdarzeń** bloku portalu, wybierz opcję **Azure Data Lake Store** z **przechwytywania dostawcy** pole.
3. W polu **Wybierz usługę Data Lake Store** określ utworzone wcześniej konto usługi Data Lake Store, a w polu **Ścieżka w usłudze Data Lake** wprowadź ścieżkę do utworzonego folderu danych.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Dodawanie lub konfigurowanie funkcji przechwytywania w istniejącym centrum zdarzeń

Przechwytywanie można skonfigurować w istniejących centrach zdarzeń, które znajdują się w przestrzeniach nazw usługi Event Hubs. Aby włączyć funkcję przechwytywania w istniejącym centrum zdarzeń lub zmienić ustawienia przechwytywania, kliknij przestrzeń nazw w celu załadowania bloku **Podstawy**, a następnie kliknij centrum zdarzeń, w którym chcesz włączyć przechwytywanie lub zmienić jego ustawienia. Na koniec kliknij **właściwości** Otwórz bloku, a następnie Edytuj ustawienia przechwytywania, jak pokazano na poniższej ilustracji:

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
