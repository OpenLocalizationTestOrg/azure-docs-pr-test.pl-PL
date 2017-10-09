---
title: "Funkcje aaaCreate danych w programie SQL Server przy użyciu programu SQL i Python | Dokumentacja firmy Microsoft"
description: "Przetwarzania danych z usługi SQL Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>Tworzenie funkcji dla danych w programie SQL Server przy użyciu języka SQL i Python
Ten dokument przedstawia sposób funkcji toogenerate dla danych przechowywanych w Maszynę wirtualną SQL Server na platformie Azure, które pomagają algorytmów wydajniej nauki hello danych. Można to zrobić przy użyciu języka SQL lub przy użyciu języka programowania, takich jak Python, które przedstawiono w tym miejscu.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach. To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Na przykład praktyczne, zalecamy skonsultowanie hello [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i odwoływać się toohello IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że masz:

* Utworzone konto magazynu platformy Azure. Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Przechowywane dane w programie SQL Server. Jeśli nie masz, zobacz [Przenieś tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) instrukcje dotyczące sposobu toomove hello dane za pomocą.

## <a name="sql-featuregen"></a>Funkcja generowania z SQL
W tej sekcji opisano sposób generowania funkcji za pomocą programu SQL:  

1. [Funkcja generowania na podstawie liczby](#sql-countfeature)
2. [Funkcja generowania binning](#sql-binningfeature)
3. [Wprowadza hello funkcji z jedną kolumną](#sql-featurerollout)

> [!NOTE]
> Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny toohello istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji hello i klucz podstawowy, który może być połączony z hello oryginalnej tabeli.
> 
> 

### <a name="sql-countfeature"></a>Funkcja generowania na podstawie liczby
W tym dokumencie przedstawiono dwa sposoby generowania funkcji count. Pierwsza metoda Hello używa warunkowego sum i drugi używa metody hello hello klauzuli 'where'. Następnie te mogą być dołączane funkcjami hello oryginalnej tabeli (przy użyciu kolumn klucza podstawowego) toohave liczba obok hello oryginalnych danych.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Funkcja generowania binning
Witaj poniższy przykład przedstawia sposób toogenerate binned funkcje przez binning (przy użyciu 5 bins) kolumny liczbowe, która może służyć jako funkcja zamiast tego:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Wprowadza hello funkcji z jedną kolumną
W tej sekcji przedstawiony sposób tooroll poza pojedyncza kolumna w tabeli toogenerate dodatkowe funkcje. przykład Witaj zakłada, że istnieje szerokości geograficznej lub długość geograficzną kolumny w tabeli hello, z którym próbujesz toogenerate funkcji.

Oto krótkie Elementarz na współrzędne/geograficznej lokalizacji danych (planować z stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Jest to przydatne toounderstand przed pole lokalizacji hello featurizing:

* znak Hello informuje NAS czy pracujemy północ lub południe, wschód lub zachód na Witaj świecie.
* Niezerowe setki cyfrę informuje, nam używamy długości, nie szerokości geograficznej!
* cyfra Hello dziesiątki daje tooabout pozycji kilometrach 1000. Udostępnia nam przydatnych informacji o jakie kontynencie lub Oceanu jesteśmy w.
* cyfra jednostki Hello (jeden stopień decimal) zapewnia stanie się kilometrach too111 (60 mil, około 69 mil). Go nam powiedzieć około jakim stanie dużych lub kraju, w którym możemy w.
* Witaj przecinku warto się too11.1 km: można odróżnić hello położenie dużych miast z sąsiednich Miasto duże.
* drugi po przecinku Hello warto się too1.1 km: go dalej oddzielić wieś jeden od hello.
* trzeci po przecinku Hello jest warto się too110 m: zidentyfikuje dużych rolnych pola lub instytucjonalnych firmy.
* czwarty po przecinku Hello jest warto się too11 m: można zidentyfikować zbiorczym ziemi. To typowy dokładność toohello można porównywać pod względem jednostki GPS Niepoprawione bez zakłóceń.
* Hello piątej po przecinku warto się too1.1 m: go odróżnić od siebie drzewa. Poziom toothis dokładność z komercyjnego jednostki GPS można uzyskać tylko z różnicowej korekty.
* szóstego po przecinku Hello warto się m: too0.11, możesz użyć tej funkcji do układania struktury szczegółowo projektowania krajobrazów, tworzenie drogi. Powinna ona więcej niż wystarczy do śledzenia przemieszczania glaciers i rzek. Można to osiągnąć, wykonując painstaking środków GPS, takich jak differentially poprawiony GPS.

informacje o lokalizacji Hello można można featurized następujące oddzielanie regionu, lokalizacji i miejscowości. Należy pamiętać, że raz także wywołać punkt końcowy REST, np. interfejsu API map Bing dostępne pod adresem `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/regionalnego informacji.

    select
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Hello w powyższej lokalizacji, na podstawie funkcje można dodatkowo korzysta z funkcji count dodatkowe toogenerate zgodnie z wcześniejszym opisem.

> [!TIP]
> Można programowo wstawić hello rekordów przy użyciu języka wybór. Może być konieczne danych hello tooinsert efektywności zapisu tooimprove fragmentów [zapoznaj się z przykładem hello toodo to w tym miejscu przy użyciu pyodbc](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> Alternatywą jest tooinsert danych przy użyciu bazy danych hello [narzędzia BCP](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Łączenie tooAzure uczenia maszynowego
Funkcja Hello nowo wygenerowane mogą być dodawane jako kolumny tabeli istniejącej tooan lub przechowywane w nowej tabeli lub połączony z oryginalnej tabeli hello do uczenia maszynowego. Funkcje mogą być generowane lub niemożliwy, jeśli już utworzone przy użyciu hello [i zaimportuj dane](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modułu w uczenie Maszynowe Azure, jak pokazano poniżej:

![czytniki uczenie maszynowe Azure](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Przy użyciu języka programowania, takich jak Python
Za pomocą funkcji toogenerate Python, gdy dane hello jest w programie SQL Server jest podobne tooprocessing dane obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure proces w przypadku danych nauki środowisku](machine-learning-data-science-process-data-blob.md). dane Hello musi załadować z bazy danych hello do ramki danych pandas toobe i następnie mogą być dalej przetwarzane. Firma Microsoft dokumentu hello proces łączenia toohello bazy danych i ładowania danych hello do ramki danych hello w tej sekcji.

Witaj następującego formatu ciągu połączenia może być bazy danych programu SQL Server tooa tooconnect używanych w języku Python za pomocą pyodbc (Zastąp servername, dbname, nazwę użytkownika i hasła o określonej wartości):

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Witaj [biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python. Poniższy kod Hello odczytuje hello wyników zwrócony z bazy danych programu SQL Server do ramki danych Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Teraz możesz pracować z hello Pandas danych ramki, co opisano w tematach [Tworzenie funkcji dla danych magazynu obiektów blob platformy Azure przy użyciu Panda](machine-learning-data-science-create-features-blob.md).

