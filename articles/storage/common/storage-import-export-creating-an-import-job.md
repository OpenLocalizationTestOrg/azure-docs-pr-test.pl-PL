---
title: aaaCreate zadania importu dla Import/Eksport Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate importu dla hello usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Tworzenie zadania importu dla hello usługi Import/Eksport Azure

Tworzenie zadania importu za pomocą hello interfejsu API REST usługi Import/Eksport Microsoft Azure hello obejmuje hello następujące kroki:

-   Przygotowywanie stacje z hello Azure narzędzie importu/eksportu.

-   Uzyskiwanie hello lokalizacji toowhich tooship hello dysku.

-   Tworzenie zadania importu hello.

-   Wysyłanie hello dysków tooMicrosoft za pomocą usługi obsługiwane operatora.

-   Uaktualnianie zadania importu hello hello szczegóły wysyłki.

 Zobacz [przy użyciu hello Import/Eksport Microsoft Azure service tooTransfer danych tooBlob magazynu](storage-import-export-service.md) Omówienie usługi Import/Eksport hello i samouczek, który demonstruje sposób toouse hello [portalu Azure](https://portal.azure.com/) toocreate i zarządzanie importowanie i eksportowanie zadań.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Przygotowywanie stacje z hello Azure narzędzie importu/eksportu

Witaj kroki tooprepare dysków dla zadania importu są hello sama czy tworzyć hello jobvia hello portalu lub za pośrednictwem hello interfejsu API REST.

Poniżej znajduje się krótki przegląd Przygotowanie stacji. Zobacz toohello [odwołania ExportTool importu Azure](storage-import-export-tool-how-to-v1.md) Aby uzyskać pełne instrukcje. Możesz pobrać hello Azure narzędzie importu/eksportu [tutaj](http://go.microsoft.com/fwlink/?LinkID=301900).

Przygotowywanie dysku obejmuje:

-   Toobe dane identyfikacyjne hello zaimportowane.

-   Identyfikowanie hello docelowego BLOB w magazynie Windows Azure.

-   Przy użyciu hello Azure narzędzie importu/eksportu toocopy Twojego tooone danych lub większej liczby dysków twardych.

 Hello Azure narzędzie importu/eksportu również spowoduje wygenerowanie pliku manifestu dla poszczególnych dysków hello, jak jest przygotowana. Plik manifestu zawiera:

-   Wyliczenie wszystkich plików hello przeznaczonych do przekazywania i mapowania hello z tooblobs tych plików.

-   Sum kontrolnych segmentów hello każdego pliku.

-   Informacje o metadanych i właściwości tooassociate hello z każdy obiekt blob.

-   Lista tootake akcji hello Jeśli obiektu blob, który jest przekazywanych ma hello takie same nazwy jako istniejącym obiektem blob w kontenerze hello. Dostępne są opcje:) Zastąp hello blob pliku hello, (b) zachować hello istniejących obiektów blob i Pomiń przekazywanie pliku hello, c) dołączyć nazwę toohello sufiksu tak, aby nie powoduje konfliktu z innymi plikami.

## <a name="obtaining-your-shipping-location"></a>Uzyskiwanie lokalizacji wysyłki

Przed utworzeniem zadania importu, należy tooobtain wysyłanie nazwy lokalizacji i adres przez wywołanie hello [lokalizacje listy](/rest/api/storageimportexport/listlocations) operacji. `List Locations`Zwraca listę lokalizacje i ich adres wysyłkowy. Można wybrać lokalizację z hello zwrócił listę i dostarczać adres toothat dysków twardych. Można również użyć hello `Get Location` hello tooobtain operacji wysyłania bezpośrednio adres dla określonej lokalizacji.

 Wykonaj kroki hello poniżej tooobtain hello wysyłanie lokalizacji:

-   Określ nazwę hello hello Lokalizacja konta magazynu. Tę wartość można znaleźć w hello **lokalizacji** na konto magazynu hello **pulpitu nawigacyjnego** w hello Azure portalu lub, którego dotyczy kwerenda dla za pomocą zarządzania usługami hello operacji interfejsu API [uzyskiwanie magazynów Właściwości konta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Pobrać hello lokalizacji, która jest dostępna tooprocess tego konta magazynu przez wywołanie hello `Get Location` operacji.

-   Jeśli hello `AlternateLocations` właściwość lokalizacji hello zawiera samą powitalnych lokalizację, a następnie jest poprawny toouse tej lokalizacji. W przeciwnym razie wywołać hello `Get Location` ponownie operację, używając jednej z hello lokalizacji alternatywnej. Hello oryginalnej lokalizacji może być tymczasowo zamknięte konserwacji.

## <a name="creating-hello-import-job"></a>Tworzenie zadania importu hello
zadania importu hello toocreate, wywołanie hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji. Konieczne będzie hello tooprovide następujących informacji:

-   Nazwa zadania hello.

-   Nazwa konta magazynu Hello.

-   Witaj wysyłania nazwy lokalizacji, uzyskane w poprzednim kroku hello.

-   Typ zadania (Importuj).

-   adres zwrotny Hello gdzie hello dyski mają być wysyłane po zakończeniu zadania importu hello.

-   Lista Hello dysków w hello zadania. Dla każdego dysku należy uwzględnić następujące informacje, który został uzyskany w kroku przygotowania dysku hello hello:

    -   dysk Hello identyfikator

    -   Witaj klucza funkcji BitLocker

    -   Ścieżka względna pliku manifestu Hello na dysku twardym powitania

    -   Witaj Base16 algorytmem wyznaczania wartości skrótu MD5 pliku manifestu

## <a name="shipping-your-drives"></a>Wysyłanie dysków
Należy wysłać swój adres toohello dysków, która pochodzi z poprzedniego kroku hello i musisz podać hello usługi Import/Eksport z hello śledzenia liczby pakietów hello.

> [!NOTE]
>  Muszą dostarczać dysków za pomocą usługi obsługiwane operatora, który dostarczy numer identyfikacyjny pakietu.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Aktualizowanie zadania importu hello z informacjami o wysyłki
Po utworzeniu numer śledzenia wywołań hello [właściwości zadania aktualizacji](/api/storageimportexport/jobs#Jobs_Update) hello tooupdate operacji wysyłania Nazwa operatora, numer śledzenia hello hello zadania i numer konta operator hello zwracany wysyłki. Opcjonalnie możesz określić liczbę hello dysków i hello Data również wysyłki.

## <a name="next-steps"></a>Następne kroki

* [Przy użyciu interfejsu API REST usługi Import/Eksport hello](storage-import-export-using-the-rest-api.md)
