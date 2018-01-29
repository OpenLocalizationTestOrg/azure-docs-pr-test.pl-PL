---
title: "Wizualizacja danych big data w usłudze Power BI w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi Microsoft Power BI do wizualizacji danych Hive przetwarzanych przez usługi Azure HDInsight."
keywords: hdinsight, hadoop, hive, interakcyjne zapytania odbc interakcyjne hive, LLAP,
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/03/2018
ms.author: jgao
ms.openlocfilehash: 8b4347fde274d0d7520ef3acbd081fdb83d7dc7d
ms.sourcegitcommit: 4bd369fc472dced985239aef736fece42fecfb3b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2018
---
# <a name="visualize-hive-data-with-microsoft-power-bi-using-odbc-in-azure-hdinsight"></a>Wizualizuj dane gałąź z usługi Microsoft Power BI przy użyciu interfejsu ODBC w usłudze Azure HDInsight

Dowiedz się, jak połączyć się za pośrednictwem sterownika ODBC w usłudze Azure HDInsight z usługi Microsoft Power BI i wizualizacji danych Hive. W tym samouczku można załadować danych z tabeli programu Hive hivesampletable do usługi Power BI. Tabela gałęzi zawiera niektóre dane użycia telefonu komórkowego. Następnie można wykreślić dane użycia na mapie world:

![HDInsight Power BI raportu mapy](./media/apache-hadoop-connect-hive-power-bi/hdinsight-power-bi-visualization.png)

Informacje dotyczą również nowe [interakcyjne zapytania](../interactive-query/apache-interactive-query-get-started.md) typ klastra. Jak nawiązać HDInsight interakcyjne zapytanie, używając zapytania bezpośredniego, zobacz [wizualizacji interakcyjne Hive zapytania danych za pomocą usługi Microsoft Power BI przy użyciu zapytania bezpośredniego w usłudze Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące elementy:

* **Klaster usługi HDInsight**. Klaster może być klastra usługi HDInsight przy użyciu Hive lub nowo wydanego klastra interakcyjne zapytania. Do tworzenia klastrów, zobacz [Utwórz klaster](apache-hadoop-linux-tutorial-get-started.md#create-cluster).
* **[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)**. Istnieje możliwość pobrania kopii z [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45331).

## <a name="create-hive-odbc-data-source"></a>Tworzenie źródła danych ODBC usługi Hive

Zobacz [źródła danych ODBC utwórz gałąź rejestru](apache-hadoop-connect-excel-hive-odbc-driver.md#create-hive-odbc-data-source).

## <a name="load-data-from-hdinsight"></a>Ładowanie danych z usługi HDInsight

W tabeli Hive hivesampletable zawiera wszystkie klastry usługi HDInsight.

1. Zaloguj się do Power BI Desktop.
2. Kliknij przycisk **Home** , kliknij pozycję **Pobierz dane** z **danych zewnętrznych** wstążki, a następnie wybierz **więcej**.

    ![Otwórz dane HDInsight Power BI](./media/apache-hadoop-connect-hive-power-bi/hdinsight-power-bi-open-odbc.png)
3. Z **Pobierz dane** okienku, kliknij przycisk **innych** z lewej strony, kliknij przycisk **ODBC** z prawej strony, a następnie kliknij przycisk **Connect** w dolnej.
4. Z **z ODBC** okienku wybierz utworzony w ostatniej sekcji Nazwa źródła danych i kliknij przycisk **OK**.
5. Z **Nawigator** okienku rozwiń węzeł **ODBC -> HIVE -> domyślny**, wybierz pozycję **hivesampletable**, a następnie kliknij przycisk **obciążenia**.

## <a name="visualize-data"></a>Wizualizuj dane

Kontynuuj w poprzedniej procedurze.

1. W okienku wizualizacje wybierz **mapy**.  Jest ikona globu.

    ![HDInsight Power BI dostosowuje raportu](./media/apache-hadoop-connect-hive-power-bi/hdinsight-power-bi-customize.png)
2. W okienku pola wybierz **kraju** i **devicemake**. Widać danych wykreślić na mapie.
3. Rozwiń węzeł mapy.

## <a name="next-steps"></a>Kolejne kroki
W tym artykule przedstawiono sposób wizualizuj dane z usługi HDInsight przy użyciu usługi Power BI.  Aby dowiedzieć się więcej, zobacz następujące artykuły:

* [Umożliwia uruchamianie zapytań Hive w usłudze Azure HDInsight Zeppelin](./../hdinsight-connect-hive-zeppelin.md).
* [Łączenie programu Excel do usługi HDInsight za pomocą sterownika ODBC firmy Microsoft Hive](./apache-hadoop-connect-excel-hive-odbc-driver.md).
* [Łączenie programu Excel do platformy Hadoop za pomocą dodatku Power Query](apache-hadoop-connect-excel-power-query.md).
* [Łączenie do usługi Azure HDInsight i uruchamianie zapytań Hive przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](apache-hadoop-visual-studio-tools-get-started.md).
* [Narzędzie Azure HDInsight dla programu Visual Studio Code](../hdinsight-for-vscode.md).
* [Przekazywanie danych do usługi HDInsight](./../hdinsight-upload-data.md).
