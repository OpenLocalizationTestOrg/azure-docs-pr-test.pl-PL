---
title: aaaConnect tooHadoop programu Excel z dodatku Power Query - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zaletą tootake składników analizy biznesowej i Użyj dodatku Power Query dla programu Excel tooaccess dane przechowywane w Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Połącz Excel tooHadoop za pomocą dodatku Power Query
Jedną z kluczowych funkcji rozwiązanie danych big data firmy Microsoft hello jest integracja hello Microsoft business intelligence (BI) składników z klastrami platformy Hadoop w usłudze Azure HDInsight. Podstawowy przykład jest hello możliwości tooconnect Excel toohello konta magazynu Azure, zawierający dane hello skojarzony z klastrem usługi Hadoop przy użyciu hello Microsoft Power Query dla dodatek programu Excel. W tym artykule przedstawiono sposób tooset się i Użyj dodatku Power Query tooquery dane skojarzone z klastrem usługi Hadoop zarządzanych za pomocą usługi HDInsight.

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć hello następujące elementy:

* **Klaster usługi HDInsight**. Zobacz tooconfigure, [Rozpoczynanie pracy z usługą Azure HDInsight][hdinsight-get-started].
* **Stacja robocza** działa system Windows 7, Windows Server 2008 R2 lub nowszym systemem operacyjnym.
* **Pakiet Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, programu Excel 2013 autonomicznych lub Office 2010 Professional Plus**.

## <a name="install-power-query"></a>Instalowanie dodatku Power Query
Dodatek Power Query można zaimportować danych, który ma zostać produkt wyjściowy lub który został wygenerowany przez zadanie Hadoop uruchomiona w klastrze usługi HDInsight.

W programie Excel 2016 dodatku Power Query zostało zintegrowane hello danych Wstążce w obszarze hello Get & sekcji transformacji. W przypadku starszych wersji programu Excel, Pobierz Microsoft Power Query dla programu Excel z hello [Microsoft Download Center] [ powerquery-download] i zainstaluj go.

## <a name="import-hdinsight-data-into-excel"></a>Importowanie danych HDInsight do programu Excel
Witaj dodatku Power Query dla programu Excel umożliwia łatwe tooimport danych z klastrem usługi HDInsight do programu Excel, gdzie narzędzi do analizy Biznesowej, takie jak PowerPivot, a następnie mapować zasilania może być tooinspect używane, analizowanie i zawierają dane hello.

**dane tooimport z klastra usługi HDInsight**

1. Otwórz program Excel.
2. Utwórz nowy, pusty skoroszyt.
3. Wykonaj następujące kroki, zależnie od wersji programu Excel hello hello:

    - Excel 2016

        - Kliknij hello **danych** menu, kliknij przycisk **Pobierz dane** z hello **Get & Przekształć dane** wstążki, kliknij przycisk **Azure z**, a następnie kliknij przycisk  **Z usługi Azure HDInsight(HDFS)**.

        ![HDI. PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Kliknij hello **dodatku Power Query** menu, kliknij przycisk **Azure z**, a następnie kliknij przycisk **z usługi Microsoft Azure HDInsight**.
   
        ![HDI. PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Uwaga:** Jeśli nie widzisz hello **dodatku Power Query** menu przejść za**pliku** > **opcje** > **Dodatki**i wybierz **dodatki COM** z listy rozwijanej hello **Zarządzaj** u dołu strony hello hello. Wybierz hello **Przejdź...**  przycisk i sprawdź, że pole hello hello dodatku Power Query dla dodatek programu Excel została sprawdzona.
       
        **Uwaga:** dodatku Power Query można też tooimport danych z systemu plików HDFS, klikając **z innych źródeł**.
4. Aby uzyskać **nazwa konta**, wprowadź nazwę hello konta magazynu obiektów Blob platformy Azure hello skojarzony z klastrem, a następnie kliknij przycisk **OK**. To konto może być hello [domyślne konto magazynu](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) lub połączonym koncie magazynu.  Hello format jest *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Aby uzyskać **klucz konta**wprowadź klucz hello hello konta magazynu obiektów Blob, a następnie kliknij przycisk **zapisać**. (Należy tooenter hello konta informacje tylko powitania po raz pierwszy uzyskać dostępu do tego magazynu.)
6. W hello **Nawigator** okienku na powitania rogu hello edytora zapytań, kliknij dwukrotnie nazwę kontenera magazynu obiektów Blob hello. Domyślnie nazwa kontenera hello jest hello sama nazwa jak nazwa klastra hello.
7. Zlokalizuj **HiveSampleData.txt** w hello **nazwa** kolumny (ścieżka folderu hello jest **... / hive/magazynu/hivesampletable/**), a następnie kliknij przycisk **binarne** na powitania po lewej HiveSampleData.txt. HiveSampleData.txt zawiera wszystkie hello klastra. Opcjonalnie można użyć własnego pliku.
   
    ![HDI. PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Jeśli chcesz, można zmienić nazwy kolumny hello. Gdy wszystko będzie gotowe, kliknij przycisk **Zamknij & załadować**.  Witaj dane zostały załadowane tooyour skoroszytu:
   
    ![HDI. PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Następne kroki
W tym artykule należy przedstawiono sposób toouse dodatku Power Query tooretrieve danych z usługi HDInsight do programu Excel. Podobnie można pobierać dane z usługi HDInsight do bazy danych SQL Azure. Możliwe jest również możliwe tooupload danych do usługi HDInsight. toolearn więcej, zobacz następujące artykuły hello:

* [Łączenie programu Excel tooHDInsight z hello sterownik Microsoft Hive ODBC][hdinsight-ODBC]
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
