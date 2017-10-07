---
title: "aaaCopy danych z obiektów blob magazynu Azure do usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj AdlCopy narzędzie toocopy danych z usługi Azure magazynu obiektów blob tooData Lake — Magazyn"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store
> [!div class="op_single_selector"]
> * [Korzystanie z narzędzia DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Korzystanie z narzędzia AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Azure Data Lake Store zapewnia narzędzia wiersza polecenia, [AdlCopy](http://aka.ms/downloadadlcopy), toocopy hello następujące źródła danych:

* Z obiektów blob magazynu Azure do usługi Data Lake Store. Nie można użyć AdlCopy toocopy danych z obiektów blob magazynu tooAzure usługi Data Lake Store.
* Dwóch kont usługi Azure Data Lake Store.

Ponadto narzędzie hello AdlCopy w dwóch różnych trybach:

* **Autonomiczny**, których narzędzie hello używa zadań hello tooperform zasobów usługi Data Lake Store.
* **Przy użyciu konta usługi Data Lake Analytics**, gdzie jednostki hello przypisane tooyour konto usługi Data Lake Analytics są operacji kopiowania hello tooperform używane. Możesz toouse tej opcji przy wyświetlaniu zadań kopiowania hello tooperform w sposób przewidywalne.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Obiektów blob magazynu Azure** kontener z niektórych danych.
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **(Opcjonalnie) konta usługi Azure Data Lake Analytics** — zobacz [Rozpoczynanie pracy z usługą Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) instrukcje dotyczące sposobu toocreate Data Lake przechowywania konta.
* **Narzędzie AdlCopy**. Zainstaluj narzędzie AdlCopy hello [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Składnia narzędzia AdlCopy hello
Użyj następującej składni toowork narzędziem AdlCopy hello hello

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

Poniżej opisano Hello parametrów w składni hello:

| Opcja | Opis |
| --- | --- |
| Element źródłowy |Określa lokalizację hello hello źródła danych w hello obiektu blob magazynu Azure. Witaj źródło może być kontenera obiektów blob, obiektu blob lub innego konta usługi Data Lake Store. |
| Docelowy |Określa hello Data Lake — Magazyn docelowy toocopy do. |
| SourceKey |Określa klucz dostępu do magazynu hello źródła obiektu blob magazynu Azure hello. Jest to wymagane tylko wtedy, gdy źródło hello jest kontenera obiektów blob lub obiektu blob. |
| Konto |**Opcjonalnie**. Użyj, jeśli chcesz, aby zadanie kopiowania hello konta toorun toouse Azure Data Lake Analytics. Jeśli opcja /Account hello w składni hello, ale nie określono konto usługi Data Lake Analytics, AdlCopy korzysta z domyślnego konta toorun hello zadania. Ponadto jeśli używasz tej opcji, należy dodać hello źródłowego (obiektu Blob magazynu Azure) i docelowego (Azure Data Lake Store) jako źródła danych dla Twojego konta usługi Data Lake Analytics. |
| Jednostki |Określa liczbę hello jednostki usługi Data Lake Analytics, które będą używane dla zadania kopiowania hello. Ta opcja jest wymagane, jeśli używasz hello **/konta** opcji konta usługi Data Lake Analytics hello toospecify. |
| wzorzec |Określa wzorzec wyrażenia regularnego, która wskazuje, które toocopy obiektów blob lub plików. AdlCopy używa dopasowania z uwzględnieniem wielkości liter. Witaj Domyślny wzorzec używany, jeśli nie określono żadnych wzorzec jest toocopy wszystkie elementy. Nie można określać wielu wzorców pliku. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Użyj danych toocopy AdlCopy (jako autonomiczna) z obiektu blob magazynu Azure
1. Otwórz wiersz polecenia i przejdź do katalogu toohello AdlCopy zainstalowanym, zwykle `%HOMEPATH%\Documents\adlcopy`.
2. Uruchom następujące polecenie toocopy hello konkretnego obiektu blob hello źródła kontenera tooa usługi Data Lake Store:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Na przykład:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] powyższej składni Hello określa hello pliku toobe tooa skopiowanego folderu w hello konta usługi Data Lake Store. Narzędzie AdlCopy tworzy folder, jeśli hello podana nazwa folderu nie istnieje.

    Można tooenter zostanie wyświetlony monit o poświadczenia hello hello subskrypcji platformy Azure, w którym masz konto usługi Data Lake Store. Zostaną wyświetlone następujące dane wyjściowe podobne toohello:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. Można także skopiować wszystkie hello obiekty BLOB z konta usługi Data Lake Store toohello jeden kontener przy użyciu hello następujące polecenie:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Na przykład:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Zagadnienia dotyczące wydajności

Jeśli kopiujesz z konta magazynu obiektów Blob Azure, może być ograniczony podczas kopiowania po stronie magazynu obiektów blob hello. To spowoduje zmniejszenie wydajności hello zadania kopiowania. toolearn więcej informacji na temat limitów hello magazynu obiektów Blob Azure, zobacz limity magazynu Azure w [subskrypcji platformy Azure i ograniczenia usługi](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>Użyj danych toocopy AdlCopy (jako autonomiczna) z innego konta usługi Data Lake Store
Można również używają danych toocopy AdlCopy dwóch kont usługi Data Lake Store.

1. Otwórz wiersz polecenia i przejdź do katalogu toohello AdlCopy zainstalowanym, zwykle `%HOMEPATH%\Documents\adlcopy`.
2. Uruchom następujące polecenie toocopy hello określonego pliku z jednego tooanother konta usługi Data Lake Store.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Na przykład:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > powyższej składni Hello określa hello pliku toobe tooa skopiowanego folderu na koncie usługi Data Lake Store docelowego hello. Narzędzie AdlCopy tworzy folder, jeśli hello podana nazwa folderu nie istnieje.
   >
   >

    Można tooenter zostanie wyświetlony monit o poświadczenia hello hello subskrypcji platformy Azure, w którym masz konto usługi Data Lake Store. Zostaną wyświetlone następujące dane wyjściowe podobne toohello:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Witaj następujące polecenie kopiuje wszystkie pliki z określonego folderu w folderze usługi Data Lake Store źródłowym hello tooa konta w miejscu docelowym hello konta usługi Data Lake Store.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Zagadnienia dotyczące wydajności

Używając AdlCopy jako autonomicznego narzędzia kopii hello jest uruchamiane na udostępnionym, Azure zarządzanych zasobów. Hello wydajności, które mogą wystąpić w tym środowisku zależy od obciążenia systemu i dostępnych zasobów. W tym trybie najlepiej nadaje się do małych transferów na zasadzie ad hoc. Brak parametrów muszą toobe dopasowane używając AdlCopy jako autonomicznego narzędzia.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Użyj danych toocopy AdlCopy (za pomocą konta usługi Data Lake Analytics)
Można również użyć usługi Data Lake Analytics konta tooData Lake — magazyn obiektów blob hello toorun AdlCopy zadania toocopy danych z magazynu Azure. Tej opcji spowoduje zwykle użyć, gdy przenieść toobe danych hello jest w zasięgu hello gigabajtów lub terabajty i ma przepływności lepsze, przewidywalną wydajność.

toouse jako źródła danych dla Twojego konta usługi Data Lake Analytics należy dodać konto usługi Data Lake Analytics toocopy AdlCopy z obiektu Blob magazynu Azure hello źródła (obiektu Blob magazynu Azure). Aby uzyskać instrukcje dotyczące dodawania konta usługi Data Lake Analytics tooyour źródeł dodatkowych danych, zobacz [źródłami danych konta zarządzania usługi Data Lake Analytics](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Jeśli jako źródło hello przy użyciu konta usługi Data Lake Analytics są kopiowane z konta usługi Azure Data Lake Store, nie trzeba tooassociate hello konta usługi Data Lake Store z hello konta usługi Data Lake Analytics. Witaj wymaganie tooassociate hello źródła magazyn z hello konta usługi Data Lake Analytics jest tylko wtedy, gdy źródło hello jest konta usługi Azure Storage.
>
>

Witaj uruchom następujące polecenie toocopy z konta usługi Data Lake Store tooa obiektu blob magazynu Azure przy użyciu konta usługi Data Lake Analytics:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Na przykład:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Podobnie Uruchom powitania po toocopy poleceń z konta usługi Data Lake Store tooa obiektu blob magazynu Azure przy użyciu konta usługi Data Lake Analytics:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Zagadnienia dotyczące wydajności

Podczas kopiowania danych w zakresie hello terabajtów, AdlCopy z kontem usługi Azure Data Lake Analytics zapewnia lepszą i bardziej przewidywalna wydajność. Hello parametr, który powinien być dopasowane jest liczbą hello Azure Data Lake Analytics jednostki toouse hello zadania kopiowania. Zwiększenie liczby hello jednostek spowoduje zwiększenie wydajności hello zadania kopiowania. Każdy toobe pliku skopiowane można użyć maksymalną jedną jednostkę. Określanie jednostki więcej niż hello liczba plików kopiowanych nie spowoduje zwiększenia wydajności.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Użyj AdlCopy toocopy danych przy użyciu dopasowanie wzorca
W tej sekcji omówiono sposób toouse AdlCopy toocopy danych ze źródła (w naszym przykładzie poniżej używamy obiektu Blob magazynu Azure) konta usługi Data Lake Store docelowego tooa za pomocą dopasowywania do wzorca. Na przykład można hello kroki toocopy wszystkie pliki z rozszerzeniem CSV z hello źródłowego obiektu blob toohello docelowego.

1. Otwórz wiersz polecenia i przejdź do katalogu toohello AdlCopy zainstalowanym, zwykle `%HOMEPATH%\Documents\adlcopy`.
2. Uruchamianie wszystkich plików hello następujące polecenie toocopy z rozszerzeniem *.csv z określonego obiektu blob z hello źródła kontenera tooa usługi Data Lake Store:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Na przykład:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Rozliczenia
* Jeśli narzędzie AdlCopy hello jest używany jako autonomiczny opłaty będą naliczane koszty wyjście do przenoszenia danych, jeśli źródło hello konta magazynu Azure nie znajduje się w hello tego samego regionu, jak hello usługi Data Lake Store.
* Jeśli używasz narzędzia AdlCopy hello z usługi Data Lake Analytics konta, standardowe [rozliczeń stawki usługi Data Lake Analytics](https://azure.microsoft.com/pricing/details/data-lake-analytics/) będą stosowane.

## <a name="considerations-for-using-adlcopy"></a>Zagadnienia dotyczące korzystania z AdlCopy
* AdlCopy (w przypadku wersji 1.0.5) obsługuje kopiowanie danych ze źródeł, które zbiorczo ma więcej niż tysięcy plików i folderów. Jednak jeśli wystąpią problemy dotyczące kopiowania dużego zestawu danych, można rozpowszechniać hello plików/folderów w różnych podfolderach i zamiast tego użyj podfoldery hello ścieżki toothose jako źródło hello.

## <a name="performance-considerations-for-using-adlcopy"></a>Zagadnienia dotyczące wydajności dla przy użyciu AdlCopy

AdlCopy obsługuje kopiowanie danych zawierających tysięcy plików i folderów. Jednak wystąpią problemy dotyczące kopiowania dużego zestawu danych, można rozpowszechniać hello plików/folderów na mniejsze podfoldery. AdlCopy został utworzony dla kopii ad hoc. Jeśli próbujesz danych toocopy cyklicznie, należy rozważyć użycie [fabryki danych Azure](../data-factory/data-factory-azure-datalake-connector.md) zapewnia pełnego zarządzania wokół hello operacji kopiowania.

## <a name="release-notes"></a>Informacje o wersji
* 1.0.13 — Jeśli kopiujesz toohello danych tego samego konta usługi Azure Data Lake Store w wielu adlcopy poleceń, nie trzeba tooreenter poświadczeń dla każdej działają. Adlcopy teraz będą buforowane tych informacji przez wiele przebiegów.

## <a name="next-steps"></a>Następne kroki
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
