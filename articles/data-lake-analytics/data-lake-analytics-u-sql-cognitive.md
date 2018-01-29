---
title: "Za pomocą funkcji kognitywnych U-SQL w usłudze Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać analizy kognitywnych możliwości w języku U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: ec48a07af0aba78f2e508bad232f34102f0c2073
ms.sourcegitcommit: ce934aca02072bdd2ec8d01dcbdca39134436359
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/08/2017
---
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a>Samouczek: Rozpoczynanie pracy z funkcjami kognitywnych U-SQL

## <a name="overview"></a>Omówienie
Kognitywnych możliwości U-SQL umożliwiają deweloperom używanie analizy put w swoich programach danych big data. 

Dostępne są następujące funkcje kognitywnych:
* Tworzenie obrazów: Wykrywanie powierzchni
* Tworzenie obrazów: Wykrywanie emocji
* Tworzenie obrazów: Wykrycia obiektów (znakowanie)
* Tworzenie obrazów: Rozpoznawania (OCR)
* Tekst: Wyodrębnianie klucza frazy
* Tekstu: Analiza wskaźniki nastrojów klientów

## <a name="how-to-use-cognitive-in-your-u-sql-script"></a>Jak używać Cognitive skryptu U-SQL

Ogólny proces jest prosty:

* Użyj instrukcji zestaw odwołania, aby włączyć funkcje kognitywnych skryptu U-SQL
* W wejściowym zestawie wierszy przy użyciu UDO kognitywnych, aby wygenerować wyjściowy, użyj procesu zestawu wierszy

### <a name="detecting-objects-in-images"></a>Wykrywanie obiektów w obrazów

Poniższy przykład pokazuje, jak używać funkcji kognitywnych do wykrycia obiektów w obrazach.

```
REFERENCE ASSEMBLY ImageCommon;
REFERENCE ASSEMBLY FaceSdk;
REFERENCE ASSEMBLY ImageEmotion;
REFERENCE ASSEMBLY ImageTagging;
REFERENCE ASSEMBLY ImageOcr;

// Get the image data

@imgs =
    EXTRACT 
        FileName string, 
        ImgData byte[]
    FROM @"/usqlext/samples/cognition/{FileName}.jpg"
    USING new Cognition.Vision.ImageExtractor();

//  Extract the number of objects on each image and tag them 

@tags =
    PROCESS @imgs 
    PRODUCE FileName,
            NumObjects int,
            Tags SQL.MAP<string, float?>
    READONLY FileName
    USING new Cognition.Vision.ImageTagger();

@tags_serialized =
    SELECT FileName,
           NumObjects,
           String.Join(";", Tags.Select(x => String.Format("{0}:{1}", x.Key, x.Value))) AS TagsString
    FROM @tags;

OUTPUT @tags_serialized
    TO "/tags.csv"
    USING Outputters.Csv();
```
Więcej przykładów można znaleźć w **przykłady U-SQL/Cognitive** w **następne kroki** sekcji.

## <a name="next-steps"></a>Następne kroki
* [U-SQL/kognitywnych próbek](https://github.com/Azure-Samples?utf8=✓&q=usql%20cognitive)
* [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL](data-lake-analytics-use-window-functions.md)
