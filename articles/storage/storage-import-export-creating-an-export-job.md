---
title: aaaCreate eksportu zadania dla Import/Eksport Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zadanie toocreate eksportu hello usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Tworzenie zadania eksportu dla hello usługi Import/Eksport Azure
Tworzenie zadania eksportu przy użyciu hello interfejsu API REST usługi Import/Eksport Microsoft Azure hello obejmuje hello następujące kroki:

-   Wybieranie hello obiektów blob tooexport.

-   Uzyskiwanie lokalizacji wysyłki.

-   Tworzenie zadania eksportu hello.

-   Wysyłanie tooMicrosoft Twojego pustych dysków za pomocą usługi obsługiwane operatora.

-   Uaktualnianie informacji o pakiecie hello hello zadanie eksportu.

-   Odbieranie hello dysków od firmy Microsoft.

 Zobacz [przy użyciu hello systemu Windows Azure Import/Eksport usługi tooTransfer danych tooBlob magazynu](storage-import-export-service.md) Omówienie usługi Import/Eksport hello i samouczek, który demonstruje sposób toouse hello [portalu Azure](https://portal.azure.com/) toocreate i zarządzanie importowanie i eksportowanie zadań.

## <a name="selecting-blobs-tooexport"></a>Wybieranie tooexport obiektów blob
 toocreate zadanie eksportu, konieczne będzie tooprovide listy mają tooexport z konta magazynu obiektów blob. Istnieje kilka sposobów tooselect obiektów blob toobe wyeksportowane:

-   Tooselect ścieżki względnej blob można użyć pojedynczego obiektu blob i wszystkie jego migawek.

-   Tooselect ścieżki względnej blob można użyć pojedynczego obiektu blob, z wyłączeniem jego migawek.

-   Można użyć ścieżki względnej obiektów blob i tooselect czasu migawki jedna migawka.

-   Można użyć tooselect prefiks obiektu blob wszystkie obiekty BLOB i migawki z hello podany prefiks.

-   Możesz wyeksportować wszystkie obiekty BLOB i migawek hello koncie magazynu.

 Aby uzyskać więcej informacji na temat określania obiektów blob tooexport, zobacz hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji.

## <a name="obtaining-your-shipping-location"></a>Uzyskiwanie lokalizacji wysyłki
Przed utworzeniem zadania eksportu, należy tooobtain wysyłanie nazwy lokalizacji i adres przez wywołanie hello [pobrać lokalizacji](https://portal.azure.com) lub [lokalizacje listy](/rest/api/storageimportexport/listlocations) operacji. `List Locations`Zwraca listę lokalizacje i ich adres wysyłkowy. Można wybrać lokalizację z hello zwrócił listę i dostarczać adres toothat dysków twardych. Można również użyć hello `Get Location` hello tooobtain operacji wysyłania bezpośrednio adres dla określonej lokalizacji.

Wykonaj kroki hello poniżej tooobtain hello wysyłanie lokalizacji:

-   Określ nazwę hello hello Lokalizacja konta magazynu. Tę wartość można znaleźć w hello **lokalizacji** na konto magazynu hello **pulpitu nawigacyjnego** w klasycznym hello portalu lub, którego dotyczy kwerenda dla za pomocą zarządzania usługami hello operacji interfejsu API [Get Właściwości konta magazynu](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Pobieranie lokalizacji hello, które są dostępne tooprocess tego konta magazynu przez wywołanie hello `Get Location` operacji.

-   Jeśli hello `AlternateLocations` właściwość lokalizacji hello zawiera samą powitalnych lokalizację, a następnie jest poprawny toouse tej lokalizacji. W przeciwnym razie wywołać hello `Get Location` ponownie operację, używając jednej z hello lokalizacji alternatywnej. Hello oryginalnej lokalizacji może być tymczasowo zamknięte konserwacji.

## <a name="creating-hello-export-job"></a>Tworzenie zadania eksportu hello
 zadanie eksportu hello toocreate, wywołanie hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji. Konieczne będzie hello tooprovide następujących informacji:

-   Nazwa zadania hello.

-   Nazwa konta magazynu Hello.

-   Witaj wysyłania nazwy lokalizacji, uzyskanych w poprzednim kroku hello.

-   Typ zadania (Eksportowanie).

-   adres zwrotny Hello gdzie hello dyski mają być wysyłane po zakończeniu zadania eksportu hello.

-   wyeksportowane Hello toobe listę obiektów blob (lub prefiksy obiektów blob).

## <a name="shipping-your-drives"></a>Wysyłanie dysków
 Następnie użyj hello Azure narzędzie importu/eksportu toodetermine hello liczba dysków należy toosend oparte na obiekty BLOB hello wybrano toobe wyeksportowany i hello rozmiar dysku. Zobacz hello [odwołania narzędzie importu/eksportu Azure](storage-import-export-tool-how-to-v1.md) szczegółowe informacje.

 Pakiet hello dysków w jednej pakietu i wysłać je toohello adres uzyskane w hello wcześniejszym kroku. Należy zwrócić uwagę hello numer pakietu kolejny krok opisany hello śledzenia.

> [!NOTE]
>  Muszą dostarczać dysków za pomocą usługi obsługiwane operatora, który dostarczy numer identyfikacyjny pakietu.

## <a name="updating-hello-export-job-with-your-package-information"></a>Trwa aktualizowanie zadania eksportu hello o informacje o pakiecie
 Po utworzeniu numer śledzenia wywołań hello [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) nazwy operatora hello tooupdated operacji i śledzenie liczby hello zadania. Opcjonalnie można określić numer hello dysków, adres zwrotny hello i hello także data wysyłki.

## <a name="receiving-hello-package"></a>Odbieranie hello pakietu
 Po przetworzeniu zadanie eksportu, dyski zostaną zwrócone tooyou z zaszyfrowanych danych. Możesz pobrać hello klucza funkcji BitLocker dla poszczególnych dysków hello przez wywołanie hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji. Następnie można odblokować dysku hello przy użyciu klucza hello. Plik manifestu dysku Hello na każdym dysku, zawiera listę hello plików hello dysku, a także hello oryginalny adres obiektu blob dla każdego pliku.

## <a name="next-steps"></a>Następne kroki

* [Przy użyciu interfejsu API REST usługi Import/Eksport hello](storage-import-export-using-the-rest-api.md)
