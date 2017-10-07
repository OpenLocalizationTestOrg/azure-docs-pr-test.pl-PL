---
title: "Funkcje aaaCreate danych klastra platformy Hadoop za pomocą zapytań Hive | Dokumentacja firmy Microsoft"
description: "Przykłady zapytań Hive, które generują funkcje w danych przechowywanych w klastrze usługi Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Tworzenie funkcji dla danych w klastrze usługi Hadoop przy użyciu zapytań Hive
Ten dokument przedstawia sposób przechowywania funkcje toocreate danych w klastrze usługi Azure HDInsight Hadoop za pomocą zapytań Hive. Tych zapytań programu Hive użyć osadzonego Hive funkcje zdefiniowane przez użytkownika (UDF), skrypty hello, dla której są udostępniane.

Funkcje toocreate potrzebnych operacji Hello można pamięci. Witaj wydajność zapytań programu Hive staje się ważniejsze w takich przypadkach i można zwiększyć przez dostrajanie niektórych parametrów. Hello dostrajanie z tych parametrów została szczegółowo opisana w sekcji końcowego hello.

Przykłady hello zapytań, które są przedstawiane są określone toohello [NYC taksówki podróży danych](http://chriswhong.com/open-data/foil_nyc_taxi/) scenariuszy znajdują się również w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Te zapytania już mieć określony schemat danych i są gotowe toobe przesłane toorun. W końcowej sekcji hello parametry, które użytkownicy można dostosować tak, aby ulepszyć wydajność zapytań programu Hive hello omówiono także.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach. To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że masz:

* Utworzone konto magazynu platformy Azure. Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop z hello usługi HDInsight.  Aby uzyskać instrukcje, zobacz [dostosować Azure klastrów usługi HDInsight Hadoop zaawansowane analizy](machine-learning-data-science-customize-hadoop-cluster.md).
* Witaj dane zostały przekazane tooHive tabel w klastrach usługi Azure HDInsight Hadoop. Jeśli nie, wykonaj [tworzenie i obciążenia tabel tooHive danych](machine-learning-data-science-move-hive-tables.md) tooHive danych tooupload najpierw tabel.
* Włączono klaster toohello dostępu zdalnego. Aby uzyskać instrukcje, zobacz [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Funkcja generowania
W tej sekcji opisano kilka przykładów hello sposoby, w którym można generowania funkcji za pomocą zapytań Hive. Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny toohello istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji hello i klucza podstawowego, który następnie może być połączony z hello oryginalnej tabeli. W tym miejscu są przedstawione przykłady hello:

1. [Funkcja generowania na podstawie częstotliwości](#hive-frequencyfeature)
2. [Ryzyko podzielone na kategorie zmiennych w klasyfikacji binarnej](#hive-riskfeature)
3. [Wyodrębnij funkcji z pola daty/godziny](#hive-datefeatures)
4. [Wyodrębnij funkcji z pola tekstowego.](#hive-textfeatures)
5. [Oblicz odległość między współrzędne GPS](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Funkcja generowania na podstawie częstotliwości
Często jest przydatne toocalculate hello częstotliwości poziomy hello podzielone na kategorie zmiennej lub częstotliwości hello niektórych kombinacji poziomy wiele zmiennych podzielone na kategorie. Użytkownicy mogą używać tych częstotliwości powitania po toocalculate skryptu:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Ryzyko podzielone na kategorie zmiennych w klasyfikacji binarnej
W klasyfikacji binarnej potrzebujemy tooconvert nieliczbowy podzielone na kategorie zmiennych w funkcje numeryczne po modeli hello jest używany tylko mieć funkcje numeryczne. Jest to realizowane przez zamianę każdy poziom nieliczbowy zagrożenie liczbowych. W tej sekcji zostanie przedstawiony niektórych ogólnego zapytań programu Hive obliczające wartości ryzyka hello (dziennika prawdopodobieństwo) podzielone na kategorie zmiennej.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

W tym przykładzie zmienne `smooth_param1` i `smooth_param2` są ustawione toosmooth hello ryzyka wartości obliczana na podstawie danych hello. Ryzyko ma zakresie -Inf Inf. Ryzyko > 0 wskazuje, czy hello prawdopodobieństwo, że kierowanych hello jest równy too1 jest większa niż 0,5.

Po obliczeniu hello ryzyka tabeli, użytkownicy mogą przypisywać Tabela tooa wartości ryzyka przez dołączenie go z tabelą ryzyka hello. Zapytanie łącząca Hive Hello została dostarczona w poprzedniej sekcji.

### <a name="hive-datefeatures"></a>Wyodrębnij funkcji z pól daty i godziny
Gałąź jest dostarczany z zestawem funkcji UDF przetwarzania pól daty i godziny. W gałęzi, hello domyślny format daty/godziny jest "RRRR MM-dd 00:00:00" ("1970-01-01-12:21:32" na przykład). W tej sekcji zostanie przedstawiony przykłady, które wyodrębnić hello dnia miesiąca, miesiąc hello z polem datetime i inne przykłady, które konwertowanie ciągu daty/godziny w formacie inne niż w domyślnym formacie hello domyślny ciąg formatu w tooa daty/godziny.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

To zapytanie Hive przyjęto założenie, że hello *&#60; pole Data i godzina >* jest w formacie daty/godziny hello domyślne.

Jeśli pól datetime nie jest hello domyślny format, do sygnatury czasowej Unix należy najpierw tooconvert hello datetime pola, a następnie czas Unix hello konwersji ciągu tooa sygnaturę daty/godziny, która jest domyślnej hello formatu. Po hello daty/godziny w domyślnym formacie, użytkownicy mogą stosować funkcje tooextract funkcji UDF datetime hello osadzonych.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

W tym zapytaniu, jeśli hello *&#60; pole daty/godziny >* ma wzorzec hello, takich jak *2015-03-26 12:04:39*, hello *"&#60; wzorzec pola datetime hello >"* powinna być `'MM/dd/yyyy HH:mm:ss'`. tootest, użytkownicy mogą uruchamiać

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Witaj *hivesampletable* w tym zapytaniu preinstalowane na wszystkich klastrach Azure HDInsight Hadoop domyślnie podczas przydzielania hello klastrów.

### <a name="hive-textfeatures"></a>Wyodrębnij funkcji z pola tekstowe
Jeśli tabelę programu Hive hello pola tekstowego, który zawiera ciąg słowa, które są rozdzielone spacjami, hello następujące zapytanie wyodrębnia hello długość ciągu hello i hello liczbę słów w ciągu hello.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Obliczanie odległości między zestawami współrzędne GPS
Zapytanie Hello podane w tej sekcji można bezpośrednio zastosowane toohello NYC taksówki podróży danych. Celem Hello to zapytanie jest tooshow jak tooapply osadzonych funkcji matematycznych w gałęzi toogenerate funkcji.

Witaj pola, które są używane w tym zapytaniu są współrzędne GPS hello odbiór i dropoff lokalizacji o nazwie *podnoszenia\_geograficzne*, *podnoszenia\_szerokości geograficznej*,  *dropoff\_geograficzne*, i *dropoff\_szerokości geograficznej*. zapytania Hello, obliczające hello bezpośredniego odległość między współrzędne odbiór i dropoff hello są:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

równania matematyczne Hello obliczające hello odległość między dwoma współrzędne GPS znajduje się na powitania <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">skryptów typu ruchome</a> lokacji utworzone przez Lapisu Peterowi. W jego Javascript hello funkcja `toRad()` jest po prostu *lat_or_lon*pi/180 *, który konwertuje tooradians stopni. W tym miejscu *lat_or_lon* jest szerokości geograficznej hello lub długość geograficzną. Ponieważ gałąź nie zawiera funkcji hello `atan2`, ale zawierają hello funkcja `atan`, hello `atan2` funkcji jest implementowany przez `atan` w hello powyżej zapytań Hive przy użyciu definicji hello w funkcji <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Pełną listę funkcji UDF embedded znajdują się w hello gałęzi **wbudowanych funkcji** sekcji na powitania <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Tematy zaawansowane: parametry Hive strojenia tooImprove szybkości zapytania
Witaj domyślnego parametru, ustawienia klastra gałęzi nie może być odpowiednie dla zapytań programu Hive hello i danych hello przetwarzania kwerend hello. W tej sekcji omówiono niektóre parametry, które użytkownicy można dostosować zwiększających hello wydajność zapytań programu Hive. Użytkownicy muszą parametru hello tooadd strojenia kwerendy przed hello zapytania przetwarzania danych.

1. **Miejsce na stercie Java**: dla zapytań obejmujących dołączenie dużych zestawów danych lub przetwarzania rekordów długi **kończy się wolne miejsce na stercie** jest jednym z typowych błędów hello. Można to dostroić przez ustawienie parametrów *mapreduce.map.java.opts* i *mapreduce.task.io.sort.mb* toodesired wartości. Oto przykład:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Ten parametr przydziela miejsce na stercie tooJava 4GB pamięci i powoduje sortowanie efektywniejsze przez przydzielanie większej ilości pamięci. Jest dobrym rozwiązaniem tooplay z tych przydziałów, jeśli każde miejsce tooheap powiązane błędy niepowodzenia zadania.

1. **Rozmiaru bloku systemu plików DFS** : ten parametr określa hello najmniejsza jednostka danych hello magazynów systemu plików. Na przykład jeśli rozmiar bloku hello systemu plików DFS to 128MB, następnie żadnych danych o rozmiarze poniżej oraz too128MB są przechowywane w jeden blok danych, który jest większy niż 128MB przydzielony dodatkowe bloki. Wybieranie rozmiaru bloku bardzo małych powoduje duże koszty Hadoop, ponieważ hello nazwa węzła ma tooprocess wiele więcej żądań toofind hello odpowiednich bloku dotyczących pliku toohello. Zalecane ustawienia po dotyczących gigabajty (lub więcej) danych jest:
   
        set dfs.block.size=128m;
2. **Optymalizacja operacji tworzenia sprzężenia w gałęzi** : podczas operacji łączenia w ramach mapy/zmniejszyć hello zazwyczaj miejsce w hello zmniejszyć fazy, czasami, znaczne zyski uzyskuje się poprzez zaplanowanie sprzężenia w fazie mapy hello (zwane również "mapjoins"). toodirect gałęzi toodo to o ile to możliwe, firma Microsoft może ustawić:
   
        set hive.auto.convert.join=true;
3. **Określanie liczby hello tooHive mapowań** : podczas Hadoop pozwala hello użytkownika tooset hello liczba reduktory, hello liczby mapowań jest zwykle nie można ustawić hello użytkownika. Lewy, umożliwiający pewien stopień kontroli tego numeru jest toochoose hello Hadoop zmiennych, *mapred.min.split.size* i *mapred.max.split.size* jako rozmiar hello map zadań zależy od:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Zazwyczaj hello wartość domyślną *mapred.min.split.size* ma wartość 0, z *mapred.max.split.size* jest **Long.MAX** i *dfs.block.size* to 64MB. Jak widać, rozmiar danych danego hello, dostrajanie parametrów "ustawienia" ich pozwala nam tootune hello liczby mapowań używane.
4. Kilka innych kolejnych **zaawansowane opcje** Hive optymalizacji wydajności są wymienione poniżej. Te pozwalają tooset hello przydzielonej pamięci toomap i zmniejszyć zadań i mogą być przydatne w Dostosowywanie wydajności. Należy pamiętać o tym hello *mapreduce.reduce.memory.mb* nie może być większy niż rozmiar pamięci fizycznej hello każdego węzła procesu roboczego w hello klastra usługi Hadoop.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

