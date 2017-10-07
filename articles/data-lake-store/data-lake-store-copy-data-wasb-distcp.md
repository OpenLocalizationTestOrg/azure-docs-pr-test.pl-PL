---
title: "aaaCopy tooand danych z WASB do usługi Data Lake Store za pomocą narzędzia Distcp | Dokumentacja firmy Microsoft"
description: "Użyj narzędzia Distcp narzędzie toocopy danych tooand z Azure magazynu obiektów blob tooData Lake — Magazyn"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Użyj narzędzia Distcp toocopy danych między obiektach blob magazynu Azure i usługi Data Lake Store
> [!div class="op_single_selector"]
> * [Korzystanie z narzędzia DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Korzystanie z narzędzia AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Po utworzeniu klastra usługi HDInsight, który ma konto usługi Data Lake Store tooa dostępu, można użyć narzędzia ekosystemu Hadoop, takie jak dane toocopy narzędzia Distcp **tooand z** magazynu klastra usługi HDInsight (WASB) do konta usługi Data Lake Store. Ten artykuł zawiera instrukcje na temat tooachieve to.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store. Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Upewnij się, że włączenie pulpitu zdalnego dla klastra hello.

## <a name="do-you-learn-fast-with-videos"></a>Czy dzięki filmom szybko się uczysz?
[Obejrzyj ten film](https://mix.office.com/watch/1liuojvdx6sie) na temat danych toocopy między obiektach blob magazynu Azure i usługi Data Lake Store za pomocą narzędzia DistCp.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Za pomocą narzędzia Distcp z klastra usługi HDInsight w systemie Linux

Klaster usługi HDInsight jest dostarczany z hello narzędzia Distcp narzędzia, które mogą być używane toocopy danych z różnych źródeł do klastra usługi HDInsight. Jeśli skonfigurowano hello HDInsight klastra toouse Data Lake Store jako dodatkowego magazynu, hello narzędzia Distcp narzędzie może być używane poza pole toocopy tooand danych z na koncie usługi Data Lake Store. W tej sekcji opisano, jak toouse hello narzędzia Distcp narzędzia.

1. Z pulpitu Użyj klastra toohello tooconnect SSH. Zobacz [Connect tooa opartych na systemie Linux klaster usługi HDInsight](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Uruchom polecenia hello z hello SSH wiersza.

2. Sprawdź, czy można uzyskać dostęp do hello Azure blob Storage (WASB). Uruchom następujące polecenie hello:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    To powinien zawierać listę zawartości obiektu blob magazynu hello.
3. Podobnie należy sprawdzić, czy mają dostęp do konta usługi Data Lake Store hello z hello klastra. Uruchom następujące polecenie hello:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    To powinien zawierać listę plików/folderów w hello konta usługi Data Lake Store.
4. Użyj narzędzia Distcp toocopy danych z tooa WASB konta usługi Data Lake Store.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Spowoduje to skopiowanie zawartości hello hello **/przykład/data/gutenberg/** folderu w WASB zbyt**/myfolder** w hello konta usługi Data Lake Store.
5. Podobnie Użyj narzędzia Distcp toocopy danych z tooWASB konta usługi Data Lake Store.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Spowoduje to skopiowanie zawartości hello **/myfolder** w hello usługi Data Lake Store za konta**/przykład/data/gutenberg/** folderu w WASB.

## <a name="performance-considerations-while-using-distcp"></a>Zagadnienia dotyczące wydajności podczas korzystania z narzędzia DistCp

Ponieważ narzędzia DistCp obiektu najniższy poziom szczegółowości pojedynczy plik, najważniejszych toooptimize parametru hello jest ustawienie hello maksymalną liczbę jednoczesnych kopii go przed usługi Data Lake Store. Jest to kontrolowane przez ustawienie hello liczby mapowań ('M ') parametr hello w wierszu polecenia. Ten parametr określa maksymalną liczbę mapowań, które będą używane toocopy danych hello. Wartość domyślna to 20.

**Przykład**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Jak ustalić liczbę hello toouse mapowań?

Oto kilka użytecznych wskazówek.

* **Krok 1: Określanie pamięć YARN** -hello pierwszym krokiem jest gdy zostanie uruchomione zadanie narzędzia DistCp hello toodetermine hello YARN pamięci toohello dostępności klastra. Te informacje są dostępne w portalu Ambari hello skojarzony z klastrem hello. Nawigacja tooYARN i wyświetlanie hello Configs kartę toosee hello YARN pamięci. tooget hello YARN pamięć, mnożenie hello YARN ilość pamięci na węzeł z hello liczba węzłów się, że masz w klastrze.

* **Krok 2: Obliczanie hello liczby mapowań** — Witaj wartość **m** jest równy toohello iloraz pamięć YARN rozdzielonych hello YARN kontenera rozmiar. Hello YARN informacje o rozmiarze kontenera jest dostępna w hello Ambari również portalu. Przejdź tooYARN i widoku hello Configs kartę hello rozmiaru kontenera YARN jest wyświetlany w tym oknie. Witaj tooarrive równości hello liczby mapowań (**m**) jest

        m = (number of nodes * YARN memory for each node) / YARN container size

**Przykład**

Załóżmy, że masz 4 węzły D14v2s hello klastra oraz chcesz tootransfer 10TB danych z różnych folderach 10. Zawiera foldery hello różnych ilości danych różni się od hello rozmiary plików w ramach każdego folderu.

* Łączna pamięć YARN — z hello portalu Ambari okaże się, że hello YARN pamięci jest 96GB dla węzła D14. Tak całkowita pamięć YARN 4 węzła klastra jest: 

        YARN memory = 4 * 96GB = 384GB

* Liczba mapowań — od hello portalu Ambari, można określić tego rozmiaru kontenera YARN hello jest 3072 D14 węzła klastra. Tak liczba mapowań to:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Jeśli inne aplikacje korzystają z pamięci, następnie możesz wybrać Użyj tooonly część klastra YARN pamięci narzędzia DistCp.

### <a name="copying-large-datasets"></a>Kopiowanie dużych zestawów danych

Po przeniesieniu hello rozmiar hello toobe zestawu danych jest bardzo duże (np. > 1TB) lub jeśli masz wiele różnych folderach, należy rozważyć użycie wielu zadań narzędzia DistCp. Nie jest prawdopodobnie nie są bardziej wydajne, ale będzie rozkładu limit hello zadania, aby w przypadku niepowodzenia wszystkie zadania wystarczy toorestart tego określonego zadania, a nie całego zadania hello.

### <a name="limitations"></a>Ograniczenia

* Narzędzia DistCp próbuje mapowań toocreate, podobne rozmiar toooptimize wydajności. Zwiększenie liczby hello mapowań może nie zawsze zwiększyć wydajność.

* Narzędzia DistCp jest ograniczona tooonly jeden mapowania na plik. W związku z tym nie powinna mieć mapowań więcej niż liczba kupionych plików. Ponieważ narzędzia DistCp można przypisać tylko jednego mapowania tooa pliku, ogranicza ilość hello współbieżności, które mogą być używane toocopy dużych plików.

* Jeśli masz niewielką liczbę dużych plików, a następnie należy rozdzielić je do 256MB pliku fragmentów toogive możesz więcej potencjalnych współbieżności. 
 
* Jeśli kopiujesz z konta magazynu obiektów Blob Azure, zadanie kopiowania może ograniczony po stronie magazynu obiektów blob hello. To spowoduje zmniejszenie wydajności hello zadania kopiowania. toolearn więcej informacji na temat limitów hello magazynu obiektów Blob Azure, zobacz limity magazynu Azure w [subskrypcji platformy Azure i ograniczenia usługi](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Zobacz też
* [Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
