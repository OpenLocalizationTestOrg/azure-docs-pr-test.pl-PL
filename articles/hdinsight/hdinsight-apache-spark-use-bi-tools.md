---
title: "aaaSpark BI za pomocą narzędzi wizualizacji danych w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użycie narzędzi do wizualizacji danych analytics przy użyciu analizy Biznesowej programu Apache Spark w klastrach HDInsight"
keywords: "Platforma spark jest Apache spark analizy biznesowej, spark analizy biznesowej, spark wizualizację danych, analiza biznesowa"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark BI z usługą Azure HDInsight przy użyciu narzędzi do wizualizacji danych

Dowiedz się, jak narzędzia toouse wizualizacji danych w takich jak Power BI i Tableau tooanalyze zestawu danych pierwotnych próbki przy użyciu Apache Spark w usłudze BI w klastrach usługi HDInsight.

> [!NOTE]
> Łączność z narzędzi do analizy Biznesowej opisane w tym artykule nie jest obsługiwana na 2.1 Spark on Azure HDInsight 3,6 Preview. Tylko Spark w wersji 1.6 i 2.0 (HDInsight 3.4, 3.5 odpowiednio) są obsługiwane.
>

W tym samouczku jest również dostępny jako notesu Jupyter w klastrze Spark w usłudze HDInsight. środowisko notesu Hello umożliwia uruchamianie hello Python wstawki z notesu hello, sama. Samouczek hello tooperform z poziomu Notes, tworzenie klastra Spark, uruchom notesu Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), a następnie uruchom notesu hello **narzędzi do analizy Biznesowej użycia z platformy Apache Spark w HDInsight.ipynb** w obszarze hello **języka Python**  folderu.

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Przygotowanie danych do wizualizacji danych Spark

W tej sekcji użyjesz hello [Jupyter](https://jupyter.org) notesu z zadań toorun klastra Spark w usłudze HDInsight, które przetwarzają przykładowe nieprzetworzone dane i zapisz go jako tabelę. Witaj przykładowych danych jest plik CSV (hvac.csv) dostępne na wszystkich klastrach domyślnie. Gdy dane są zapisywane jako tabelę, w następnej sekcji hello firma Microsoft BI narzędzia tooconnect toohello tabeli i wykonywać wizualizacje danych.

> [!NOTE]
> Jeśli przeprowadzasz hello kroki opisane w tym artykule po ukończeniu instrukcjami hello [uruchamianie interakcyjnych zapytań w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-load-data-run-query.md), możesz pominąć tooStep 8 poniżej.
>

1. Z hello [portalu Azure](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.   

2. W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

   > [!NOTE]
   > Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Utwórz notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.

    ![Tworzenie notesu Jupyter dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "tworzenie notesu Jupyter do analizy Biznesowej programu Apache Spark")

4. Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.

    ![Podaj nazwę notesu powitania dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "podanie nazwę notesu hello Apache Spark w usłudze BI")

5. Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie. konteksty Spark i Hive Hello są utworzony automatycznie po uruchomieniu pierwszej komórki kodu hello. Możesz zacząć od importowania typów hello wymaganych dla tego scenariusza. toodo tak, umieść kursor hello w komórce hello i naciśnij klawisze **SHIFT + ENTER**.

        from pyspark.sql import *

6. Załaduj przykładowe dane do tabeli tymczasowej. Podczas tworzenia klastra Spark w usłudze HDInsight, hello przykładowy plik danych **hvac.csv**, jest skopiowany toohello skojarzone konto magazynu w obszarze **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    W pustej komórce Wklej hello następujący fragment kodu i naciśnij klawisz **SHIFT + ENTER**. Ta Wstawka kodu rejestruje dane hello w tabeli o nazwie **hvac**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Sprawdź, czy tabela hello została pomyślnie utworzona. Można użyć hello `%%sql` Magiczna toorun zapytań Hive bezpośrednio. Aby uzyskać więcej informacji na temat hello `%%sql` magic i innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Pojawić się dane wyjściowe, jak pokazano poniżej:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Tylko hello tabel, które mają wartość false w obszarze hello **isTemporary** kolumny są są przechowywane w hello potrzeby magazynu metadanych, które są dostępne z narzędzi do analizy Biznesowej hello tabele programu hive. W tym samouczku połączymy toohello **hvac** utworzyliśmy tabeli.

8. Sprawdź, czy hello zawierającej dane hello przeznaczone. W pustej komórce w notesie hello, skopiuj następujące hello fragment kodu i naciśnij klawisz **SHIFT + ENTER**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Zamknij hello notesu toorelease hello zasobów. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.

## <a name="powerbi"></a>Użyj usługi Power BI dla Spark wizualizacji danych

> [!NOTE]
> Ta sekcja ma zastosowanie tylko do wersji 1.6 Spark w usłudze HDInsight w wersji 3.4 i 2.0 Spark w usłudze HDInsight 3.5.
>
>

Po zapisaniu hello danych jako tabelę, za pomocą usługi Power BI tooconnect toohello danych i wizualizacji go toocreate raporty, pulpity nawigacyjne,... itd.

1. Upewnij się, że masz dostęp tooPower BI. Możesz uzyskać bezpłatne sprawdzenie subskrypcji usługi Power BI z [http://www.powerbi.com/](http://www.powerbi.com/).

2. Zaloguj się za[usługi Power BI](http://www.powerbi.com/).

3. Hello dolnej części okienka po lewej stronie powitania kliknij **Pobierz dane**.

4. Na powitania **Pobierz dane** w obszarze **importowanie danych lub łączenie tooData**, dla **baz danych**, kliknij przycisk **uzyskać**.

    ![Pobieranie danych do usługi Power BI dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "pobieranie danych do usługi Power BI dla Apache Spark w usłudze BI")

5. Na następnym ekranie powitania kliknij **Spark w usłudze Azure HDInsight** , a następnie kliknij przycisk **Connect**. Po wyświetleniu monitu wprowadź adres URL klastra hello (`mysparkcluster.azurehdinsight.net`) i hello poświadczenia tooconnect toohello klastra.

    ![Połącz tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "połączyć tooApache Spark BI")

    Po nawiązaniu połączenia hello usługi Power BI uruchamia importowania danych z hello klastra Spark w usłudze HDInsight.

6. Usługa Power BI importuje dane hello i dodaje **Spark** zestawu danych w obszarze hello **zestawów danych** nagłówka. Kliknij przycisk tooopen zestawu danych hello nowe dane hello toovisualize arkusza. Można również zapisać arkusza hello jako raport. Arkusz z hello toosave **pliku** menu, kliknij przycisk **zapisać**.

    ![Apache Spark w usłudze BI kafelka pulpitu nawigacyjnego usługi Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark w usłudze BI kafelka pulpitu nawigacyjnego usługi Power BI")
7. Zwróć uwagę, że hello **pola** lista po prawej stronie powitania listy hello **hvac** tabeli utworzony wcześniej. Rozwiń hello tabeli toosee hello pola w tabeli hello zgodnie z definicją w notesie wcześniej.

      ![Lista tabel na pulpicie nawigacyjnym Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "listy tabel na pulpicie nawigacyjnym Apache Spark w usłudze BI")

8. Tworzenie wizualizacji tooshow hello odchylenie temperatury docelowy rzeczywiste temperatury dla każdego tworzenia. Wybierz dane yoru toovisualize, **obszaru wykresu** (pokazywaną w czerwonym prostokątem). toodefine hello osi, przeciągnij i upuść hello **BuildingID** pole w obszarze **osi**, i **ActualTemp**/**TargetTemp** pola w obszarze **wartość**.

    ![Tworzenie wizualizacji danych przy użyciu Apache Spark w usłudze BI Spark](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "wizualizacje danych utworzyć Spark przy użyciu Apache Spark w usłudze BI")

9. Domyślnie wizualizacji hello przedstawia sumę hello **ActualTemp** i **TargetTemp**. Witaj oba pola z listy rozwijanej hello wybierz **średni** tooget średniej rzeczywistego i temperatury docelowy dla obu budynków.

    ![Tworzenie wizualizacji danych przy użyciu Apache Spark w usłudze BI Spark](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "wizualizacje danych utworzyć Spark przy użyciu Apache Spark w usłudze BI")

10. Twoje wizualizacji danych powinny być podobne jedną toohello hello zrzucie ekranu. Przesuń kursor nad hello wizualizacji tooget podpowiedzi z właściwymi danymi.

    ![Tworzenie wizualizacji danych przy użyciu Apache Spark w usłudze BI Spark](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "wizualizacje danych utworzyć Spark przy użyciu Apache Spark w usłudze BI")

11. Kliknij przycisk **zapisać** z hello menu z góry i podaj nazwę raportu. Możesz również przypiąć hello visual. Przypnij wizualizacje, są przechowywane na pulpicie nawigacyjnym, więc można śledzić hello najpóźniejszą wartość jeden rzut oka.

   Możesz dodać dowolną liczbę wizualizacje chcesz hello tego samego zestawu danych i przypiąć je toohello, odwiedź pulpit nawigacyjny migawki danych. Ponadto klastry Spark w usłudze HDInsight są połączone tooPower połączyć BI bezpośrednio. Daje to pewność, że usługi Power BI ma zawsze hello większości aktualne dane z klastra, nie trzeba odświeża tooschedule hello zestawu danych.

## <a name="tableau"></a>Za pomocą pulpitu Tableau dla Spark wizualizacji danych

> [!NOTE]
> Ta sekcja dotyczy tylko klastry Spark 1.5.2 utworzone w usłudze Azure HDInsight.
>
>

1. Zainstaluj [pulpitu Tableau](http://www.tableau.com/products/desktop) na komputerze hello, w którym są uruchomione w tym samouczku Apache Spark w usłudze BI.

2. Upewnij się, że ten komputer ma również zainstalowanego sterownika Microsoft Spark ODBC. Można zainstalować sterownik hello z [tutaj](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Uruchom Tableau pulpitu. W okienku po lewej stronie powitania, z listy hello tooconnect serwera, kliknij przycisk **Spark SQL**. Jeśli Spark SQL nie znajduje się domyślnie w okienku po lewej stronie powitania, możesz go znaleźć, kliknij przycisk **więcej serwerów**.
2. W powitalne okno dialogowe połączenia Spark SQL, podaj wartości hello, jak pokazano w hello zrzut ekranu, a następnie kliknij przycisk **OK**.

    ![Połącz tooa klastra Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa klastra Apache Spark w usłudze BI")

    Witaj list rozwijanych uwierzytelniania **usługi Microsoft Azure HDInsight** opcjonalnie tylko w przypadku zainstalowania hello [sterownika Microsoft Spark ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) na komputerze hello.
3. Na następnym ekranie powitania od hello **schematu** listy rozwijanej, kliknij przycisk hello **znaleźć** ikonę, a następnie kliknij przycisk **domyślne**.

    ![Znaleźć schematu dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Znajdź schematu dla Apache Spark w usłudze BI")
4. Dla hello **tabeli** kliknij hello **znaleźć** ikonę ponownie toolist wszystkie hello Hive tabel dostępnych w klastrze hello. Powinny pojawić się hello **hvac** tabeli zostały utworzone wcześniej za pomocą notesu hello.

    ![Znajdź tabeli dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "tabeli Znajdź Apache Spark w usłudze BI")
5. Przeciągnij i upuść górnej liście toohello tabeli hello na powitania prawo. TABLEAU importuje dane hello i wyświetla schematu hello jak wyróżniono hello czerwonym polem.

    ![Dodawanie tabel tooTableau dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "dodać tooTableau tabel dla Apache Spark w usłudze BI")
6. Kliknij przycisk hello **Sheet1 —** karty u dołu hello w lewo. Należy wizualizacji, pokazujący hello średni docelowy i rzeczywistego temperatur w budynkach wszystkie dla każdego dnia. Przeciągnij **data** i **identyfikator budynku** zbyt**kolumn** i **rzeczywiste Temp**/**Temp docelowej**za**wierszy**. W obszarze **znaczniki**, wybierz pozycję **obszaru** toouse obszaru mapy do wizualizacji danych platformy Spark.

     ![Dodawanie pól do wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Dodawanie pól do wizualizacji danych Spark")
7. Domyślnie program hello temperatury pola są wyświetlane jako agregacji. Jeśli zamiast tego chcesz tooshow hello średnia temperatura, możesz to zrobić z rozwijanej hello, jak pokazano poniżej.

    ![Zająć średnia temperatura wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "zająć średnia temperatura Spark wizualizacji danych")

8. Można również super skonfigurować jedną mapę temperatury ponad hello innych tooget lepszego działania różnica między temperatury rzeczywiste i docelowe. Przenieś hello myszy toohello rogu hello niższe obszaru mapy, dopóki Zobacz kształtu uchwyt hello wyróżnione kolorem czerwonym kółku. Przeciągnij toohello mapy hello innych mapy hello top i wersji hello myszy po wyświetleniu kształtu hello wyróżnione kolorem czerwonym prostokątem.

    ![Scal mapy do wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "scalania mapy dla Spark wizualizacji danych")

     Twoje wizualizacji danych należy zmieniać, jak pokazano w hello zrzut ekranu:

    ![Dane wyjściowe TABLEAU do wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau danych wyjściowych Spark wizualizacji danych")
9. Kliknij przycisk **zapisać** toosave hello arkusza. Można tworzyć pulpity nawigacyjne i Dodaj jeden lub więcej arkuszy tooit.

## <a name="next-steps"></a>Następne kroki

Do tej pory przedstawiono sposób toocreate klastra, Utwórz tooquery Spark danych ramki, a następnie przejść danych z narzędzi do analizy Biznesowej. Teraz można przeglądać informacje dotyczące sposobu toomanage hello zasobów klastra i debugowania zadania, które są uruchomione w klastrze Spark w usłudze HDInsight.

* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

