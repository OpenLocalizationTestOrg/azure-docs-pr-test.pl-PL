---
title: aaaExplore danych maszyny wirtualnej w programu SQL Server na platformie Azure | Dokumentacja firmy Microsoft
description: Jak tooexplore dane przechowywane na maszynie Wirtualnej z programu SQL Server na platformie Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Eksplorowanie danych maszyny wirtualnej programu SQL Server na platformie Azure
W tym dokumencie opisano sposób tooexplore dane przechowywane na maszynie Wirtualnej z programu SQL Server na platformie Azure. Można to zrobić przy użyciu języka programowania, takich jak Python lub wrangling danych przy użyciu programu SQL.

następujące Hello **menu** łączy tootopics opisujące, jak toouse narzędzia tooexplore danych z różnych środowiskach magazynu. To zadanie jest etapem hello Cortana Analytics procesu (CAP).

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> instrukcje SQL próbki Hello w tym dokumencie założono, że dane są w programie SQL Server. Jeśli nie, zobacz toohello chmury danych nauki procesu mapy toolearn jak toomove Twojego tooSQL danych serwera.
> 
> 

## <a name="sql-dataexploration"></a>Eksplorowanie danych SQL za pomocą skryptów SQL
Poniżej przedstawiono kilka przykładowe skrypty SQL, które mogą być używane tooexplore magazyny danych w programie SQL Server.

1. Zliczanie hello uwagi na dzień
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Pobierz poziomy hello w kolumnie podzielone na kategorie
   
    `select  distinct <column_name> from <databasename>`
3. Pobierz hello podaną liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Pobierz dystrybucji hello kolumn wartości liczbowych
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Na przykład praktyczne, można użyć hello [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i odwoływać się toohello IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.
> 
> 

## <a name="python"></a>Eksplorowanie danych SQL za pomocą języka Python
Przy użyciu języka Python tooexplore danych i funkcji generowania hello danych jest w programie SQL Server jest podobne tooprocessing dane obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md). dane Hello musi załadować z bazy danych hello do pandas DataFrame toobe i następnie mogą być dalej przetwarzane. Firma Microsoft dokumentu hello proces łączenia toohello bazy danych i ładowania danych hello do hello DataFrame w tej sekcji.

Witaj następującego formatu ciągu połączenia może być bazy danych programu SQL Server tooa tooconnect używanych w języku Python za pomocą pyodbc (Zastąp servername, dbname nazwy użytkownika i hasła o określonej wartości):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Witaj [biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python. Witaj następujący kod odczytuje hello wyników zwrócony z bazy danych programu SQL Server do ramki danych Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Teraz możesz pracować z hello Pandas DataFrame, jak to opisano w temacie hello [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Proces Cortana analityka w przykładzie akcji
Przykład wskazówki na trasie hello Cortana Analytics procesu przy użyciu publicznego zestawu danych, zobacz [hello proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

