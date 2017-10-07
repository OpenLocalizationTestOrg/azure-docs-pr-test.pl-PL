---
title: "aaaDiagnostics i błąd odzyskiwania dla zadań Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable pełne rejestrowanie dla programu Microsoft Azure Import/Eksport usługi zadania."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Diagnostyka i błąd odzyskiwania dla zadań Import/Eksport Azure
Dla każdego dysku przetwarzane hello usługi Import/Eksport Azure tworzy dziennik błędów w hello skojarzone konto magazynu. Można również włączyć pełne rejestrowanie przez ustawienie hello `LogLevel` właściwości zbyt`Verbose` podczas wywoływania metody hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji.

 Domyślnie dzienniki są zapisywane tooa kontener o nazwie `waimportexport`. Określ inną nazwę, przez ustawienie hello `DiagnosticsPath` właściwości podczas wywoływania metody hello `Put Job` lub `Update Job Properties` operacji. Witaj dzienniki są przechowywane jako blokowych obiektów blob z następującą konwencją hello: `waies/jobname_driveid_timestamp_logtype.xml`.

 Możesz pobrać hello URI hello dzienników zadania przez wywołanie hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji. Hello identyfikatora URI dla pełnego dziennika hello jest zwracany w hello `VerboseLogUri` właściwości dla każdego dysku, gdy hello identyfikator URI do dziennika błędów hello jest zwracany w hello `ErrorLogUri` właściwości.

Możesz użyć hello rejestrowania danych tooidentify hello następujące problemy.

## <a name="drive-errors"></a>Błędy dysku

Witaj w poniższych elementach sklasyfikowanych jako błędy dysku:

-   Błędy podczas uzyskiwania dostępu do lub odczytywania hello pliku manifestu

-   Niepoprawne klucze funkcji BitLocker

-   Błędy odczytu/zapisu dysków

## <a name="blob-errors"></a>Błędy obiektów blob

Witaj w poniższych elementach sklasyfikowanych jako błędy obiektów blob:

-   Nazwy lub nieprawidłowa / sprzeczna obiektów blob

-   Brakujące pliki

-   Nie znaleziono obiektu blob

-   Skrócona plików (hello plików na dysku hello są mniejsze niż określona w manifeście hello)

-   Uszkodzony plik zawartości (dla zadania importu wykrył z sumy kontrolnej MD5)

-   Pliki metadanych i właściwości uszkodzony obiekt blob (wykrył z sumy kontrolnej MD5)

-   Niepoprawny schemat dla właściwości obiektu blob hello i/lub pliki metadanych

Może to być przypadki, w którym niektórych części zadania importu lub eksportu nie zostało prawidłowo wykonane, hello ogólne zadanie nadal zakończy pracę. W takim przypadku możesz przekazać lub pobrać hello Brak fragmentów danych hello za pośrednictwem sieci, lub można utworzyć nowe dane hello tootransfer zadania. Zobacz hello [odwołania narzędzie importu/eksportu Azure](storage-import-export-tool-how-to-v1.md) toolearn jak toorepair hello danych za pośrednictwem sieci.

## <a name="next-steps"></a>Następne kroki

* [Przy użyciu interfejsu API REST usługi Import/Eksport hello](storage-import-export-using-the-rest-api.md)
