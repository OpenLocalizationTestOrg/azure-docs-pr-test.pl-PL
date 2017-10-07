---
title: "aaaExtend U-SQL skrypty języka Python w usłudze Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kod toorun Python skryptów U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Samouczek: Rozpoczynanie pracy z rozszerzanie U-SQL z języka Python

Rozszerzenia języka Python dla U-SQL Włącz deweloperzy tooperform równoległemu wykonywanie kodu języka Python. Witaj poniższy przykład przedstawia hello podstawowe kroki:

* Użyj hello `REFERENCE ASSEMBLY` rozszerzenia języka Python tooenable instrukcji hello skryptu U-SQL
* Przy użyciu hello `REDUCE` operacji toopartition hello wprowadzić dane dla klucza
* Hello rozszerzenia języka Python dla U-SQL zawierają wbudowane reduktor (`Extension.Python.Reducer`) uruchomione na każdy wierzchołek przypisane toohello reduktor kodu języka Python
* Hello skryptu U-SQL zawiera osadzone hello Python kod, który ma funkcji o nazwie `usqlml_main` akceptuje pandas DataFrame jako dane wejściowe i zwraca pandas DataFrame jako dane wyjściowe.

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Jak Python integruje się z języka U-SQL

### <a name="datatypes"></a>Typy danych

* Ciąg, jak i numeryczne kolumny z U-SQL są konwertowane na — między Pandas i języka U-SQL
* U-SQL wartości null są tooand przekonwertowany z Pandas `NA` wartości

### <a name="schemas"></a>Schematy

* Wektory indeksu w Pandas nie są obsługiwane w języku U-SQL. Wszystkie ramki danych wejściowych w funkcji Python hello zawsze ma 64-bitowych indeksu numerycznych od 0 do hello liczbę wierszy pomniejszonej o 1. 
* Zestaw danych skryptu U-SQL nie mogą mieć zduplikowanych nazw kolumn
* U-SQL nazwy kolumn zestawów danych, które nie są ciągami. 

### <a name="python-versions"></a>Wersji języka Python
Obsługiwane jest tylko Python 3.5.1 (skompilowany dla systemu Windows). 

### <a name="standard-python-modules"></a>Standardowe moduły języka Python
Uwzględniane są wszystkie moduły hello standard języka Python.

### <a name="additional-python-modules"></a>Dodatkowe moduły języka Python
Oprócz hello standardowych bibliotek języka Python, uwzględniono kilka bibliotek często używane python:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Komunikaty o wyjątkach
Obecnie Wystąpił wyjątek w kodzie języka Python jest wyświetlany jako błąd rodzajowy wierzchołka. W przyszłości hello komunikaty o błędach zadań U-SQL hello wyświetli komunikat o wyjątku hello Python.

### <a name="input-and-output-size-limitations"></a>Dane wejściowe i ograniczenia rozmiaru danych wyjściowych
Każdy wierzchołek ma ograniczoną ilość pamięci przypisana tooit. Obecnie ten limit jest 6 GB dla funkcji Aktualizacje automatyczne. Ponieważ hello DataFrames wejściowych i wyjściowych musi istnieć w pamięci w kodzie języka Python hello, łączny rozmiar hello hello danych wejściowych i wyjściowych nie może przekroczyć 6 GB.

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL](data-lake-analytics-use-window-functions.md)

