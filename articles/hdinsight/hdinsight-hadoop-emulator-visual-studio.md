---
title: aaaData Lake tools dla programu Visual Studio z Hortonworks piaskownicy - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure Data Lake tools dla programu Visual Studio z piaskownicy Hortonworks hello uruchomionych w lokalnej maszyny Wirtualnej. Z tych narzędzi można tworzyć i uruchamiania zadań Hive i Pig na piaskownicy hello i dane wyjściowe zadania w widoku i historii."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Za pomocą hello Azure Data Lake tools dla programu Visual Studio hello Hortonworks piaskownicy

Usługa Azure Data Lake zawiera narzędzia do pracy z ogólnym klastrów platformy Hadoop. Ten dokument zawiera kroki hello potrzebnych narzędzi Data Lake hello toouse z hello piaskownicy Hortonworks uruchomiony na lokalnej maszynie wirtualnej.

Użycie hello piaskownicy Hortonworks umożliwia toowork z platformą Hadoop lokalnie na środowiska deweloperskiego. Po opracowaniu rozwiązania, a toodeploy go na dużą skalę, można przenieść klastra usługi HDInsight tooan.

## <a name="prerequisites"></a>Wymagania wstępne

* Witaj Hortonworks piaskownicy, działających w maszynie wirtualnej na środowiska deweloperskiego. Ten dokument został zapisany i przetestowana piaskownicy hello uruchomionych w Oracle VirtualBox. Aby uzyskać informacje na temat konfigurowania hello piaskownicy, zobacz hello [wprowadzenie hello Hortonworks piaskownicy.](hdinsight-hadoop-emulator-get-started.md) dokument.

* Visual Studio 2013, Visual Studio 2015 lub Visual Studio 2017 (dowolna wersja).

* Witaj [zestawu Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/) 2.7.1 lub nowszej.

* Witaj [Azure Data Lake tools dla Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Konfigurowanie haseł dla hello piaskownicy

Upewnij się, tym powitalne Hortonworks piaskownicy jest uruchomiona. Następnie wykonaj kroki hello hello [wprowadzenie w hello piaskownicy Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) dokumentu. Te kroki konfigurowania hello hasło hello SSH `root` konta i hello Ambari `admin` konta. Te hasła są używane podczas łączenia toohello piaskownicy w programie Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Połącz hello narzędzia toohello piaskownicy

1. Otwórz program Visual Studio, wybierz **widoku**, a następnie wybierz **Eksploratora serwera**.

2. Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello **HDInsight** wpis, a następnie wybierz **połączyć tooHDInsight emulatora**.

    ![Zrzut ekranu z Eksploratora serwera, z tooHDInsight Connect emulatora wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. Z hello **połączyć tooHDInsight emulatora** okna dialogowego wprowadź hasło hello skonfigurowane dla narzędzia Ambari.

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją pole tekstowe hasła](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Wybierz **dalej** toocontinue.

4. Użyj hello **hasło** hasło hello tooenter pola skonfigurowanych hello `root` konta. Pozostaw hello innych pól na powitania wartości domyślnej.

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją pole tekstowe hasła](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Wybierz **dalej** toocontinue.

5. Poczekaj, aż weryfikacji hello toofinish usług. W niektórych przypadkach sprawdzanie poprawności może zakończyć się niepowodzeniem i monit tooupdate hello konfiguracji. Jeśli weryfikacja zakończy się niepowodzeniem, wybierz **aktualizacji**i zaczekaj, aż hello konfiguracji i weryfikacji dla hello toofinish usługi.

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnionym przycisku Aktualizuj](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > proces aktualizacji Hello używa powitalne toomodify Ambari toowhat konfiguracji Hortonworks piaskownicy jest oczekiwane przez hello usługi Data Lake tools dla programu Visual Studio.

6. Po zakończeniu sprawdzania poprawności, wybierz **Zakończ** toocomplete konfiguracji.
    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją przycisk Zakończ](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > W zależności od szybkości hello Środowisko deweloperskie i hello ilość pamięci przydzielonej maszynie wirtualnej toohello ona potrwać kilka minut tooconfigure i zweryfikować hello usług.

Po wykonaniu tych kroków, masz teraz **lokalnego klastra usługi HDInsight** wpis w Eksploratorze serwera w obszarze hello **HDInsight** sekcji.

## <a name="write-a-hive-query"></a>Napisz zapytanie Hive

Gałąź zapewnia języka przypominającego SQL kwerendy (HiveQL) do pracy z danych strukturalnych. Użyj hello następujące czynności toolearn jak toorun na żądanie zapytania względem hello lokalnym klastrem.

1. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy wpis hello hello klastra lokalnego dodanego wcześniej, a następnie wybierz **Napisz zapytanie Hive**.

    ![Zrzut ekranu z Eksploratora serwera zapisu wyróżnione zapytanie Hive](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Pojawi się okno nowego zapytania. W tym miejscu można szybko zapisu i przesyłanie klastra lokalnego toohello zapytania.

2. W nowym oknie zapytania hello wprowadź hello następujące polecenie:

        select count(*) from sample_08;

    Kwerenda hello toorun, wybierz opcję **przesyłania** u góry hello hello okna. Pozostaw hello inne wartości (**partii** i nazwa serwera) na powitania wartości domyślne.

    ![Zrzut ekranu okna zapytań, przycisk Prześlij hello wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    Można również użyć hello menu rozwijanym obok zbyt**przesyłania** tooselect **zaawansowane**. Zaawansowane opcje pozwalają tooprovide dodatkowe opcje podczas przesyłania zadania hello.

    ![Zrzut ekranu przedstawia skryptu, okno dialogowe](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Po przesłaniu zapytania hello jest wyświetlany stan zadania hello. Stan zadania Hello Wyświetla informacje o zadaniu hello jest przetwarzany przez Hadoop. **Stan zadania** zawiera stan hello hello zadania. Stan Hello jest okresowo aktualizowana lub skorzystać z hello Odśwież ikona toorefresh hello stan ręcznie.

    ![Okno dialogowe zrzut ekranu widoku zadania, z wyróżnioną pozycją stan zadania](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Po hello **stan zadania** zmiany zbyt**zakończone**, zostanie wyświetlony skierowany acykliczne Graph (DAG). Ten schemat przedstawia ścieżka wykonywania hello, określony przez Tez podczas przetwarzania zapytania Hive hello. Tez jest hello domyślnego wykonywania aparatu gałęzi w klastrze lokalnym hello.

    > [!NOTE]
    > Tez jest to domyślna hello, korzystając z klastrów usługi HDInsight opartych na systemie Linux. Nie jest domyślnym hello w usłudze HDInsight z systemu Windows. toouse go, należy dodać wiersz hello `set hive.execution.engine = tez;` toohello początku zapytania Hive.

    Użyj hello **dane wyjściowe zadania** link tooview hello w danych wyjściowych. W takim przypadku jest 823, hello liczbę wierszy w tabeli sample_08 hello. Można wyświetlić informacje diagnostyczne o zadaniu hello przy użyciu hello **dziennik zadań** i **Pobierz dziennik YARN** łącza.

4. Można również uruchamiać zadania Hive interaktywnego, zmieniając hello **partii** pola zbyt**Interactive**. Następnie wybierz **Execute**.

    ![Zrzut ekranu interakcyjne i wykonywanie przycisków wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Interakcyjne zapytania strumieni hello dziennika danych wyjściowych wygenerowanych podczas przetwarzania toohello **danych wyjściowych serwera HiveServer2** okna.

    > [!NOTE]
    > Witaj informacji jest hello takie same, który jest dostępny z hello **dziennik zadań** link po zakończeniu zadania.

    ![Zrzut ekranu przedstawiający pliku dziennika](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Utwórz projekt Hive

Można również utworzyć projekt, który zawiera wiele skryptów Hive. Użyj projektu, gdy pokrewne skrypty lub mają toostore skryptów w systemie kontroli wersji.

1. W programie Visual Studio, wybierz **pliku**, **nowy**, a następnie **projektu**.

2. Z listy hello projektów, rozwiń węzeł **szablony**, rozwiń węzeł **usługi Azure Data Lake**, a następnie wybierz **gałąź (HDInsight)**. Wybierz z listy hello szablonów **Hive próbki**. Wprowadź nazwę i lokalizację, a następnie wybierz **OK**.

    ![Wyróżnione okno zrzut ekranu nowego projektu, przy użyciu usługi Azure Data Lake, HIVE, przykładowe Hive i OK](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Witaj **Hive próbki** projekt zawiera dwa skrypty **WebLogAnalysis.hql** i **SensorDataAnalysis.hql**. Można kierować te skrypty, używając hello sam **przesyłania** u góry hello hello okna.

## <a name="create-a-pig-project"></a>Utwórz projekt usługi Pig

Gałąź zawiera języka przypominającego SQL do pracy z danych strukturalnych, natomiast Pig działanie polega na przekształcenia danych. Pig zapewnia języka (Pig Latin), która pozwala toodevelop potoku transformacji. toouse Pig z lokalnym klastrem hello, wykonaj następujące kroki:

1. Otwórz program Visual Studio i wybierz **pliku**, **nowy**, a następnie **projektu**. Z listy hello projektów, rozwiń węzeł **szablony**, rozwiń węzeł **usługi Azure Data Lake**, a następnie wybierz **Pig (HDInsight)**. Wybierz z listy hello szablonów **aplikacji Pig**. Wprowadź nazwę lokalizacji, a następnie wybierz **OK**.

    ![Okno zrzut ekranu nowego projektu, przy użyciu usługi Azure Data Lake, Pig, Pig, aplikacji i OK, wyróżniony](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Wprowadź hello następującego tekstu jako zawartość hello hello **script.pig** pliku, który został utworzony z tego projektu.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Pig używa innego języka niż Hive, sposób uruchamiania zadań hello jest jednolita obu językach za pośrednictwem hello **przesyłania** przycisku. Wybór hello listy rozwijanej obok **przesyłania** Wyświetla okno dialogowe Zaawansowane przesyłania programu Pig.

    ![Zrzut ekranu przedstawia skryptu, okno dialogowe](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. Stan zadania Hello i danych wyjściowych będzie również wyświetlana, hello takie same jak zapytań programu Hive.

    ![Zrzut ekranu przedstawiający zakończonych zadań Pig](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Wyświetl zadania

Narzędzia Data Lake pozwalają również tooeasily Wyświetl informacje o zadaniach, które zostały uruchomione na platformie Hadoop. Użyj następujących hello kroki toosee hello zadania, które zostały uruchomione w klastrze lokalnym hello.

1. Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy klaster lokalny hello, a następnie wybierz **Wyświetl zadania**. Zostanie wyświetlona lista zadań, które zostały przesłane toohello klastra.

    ![Zrzut ekranu z Eksploratora serwera, z wyróżnioną pozycją zadaniami widoku](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Z listy hello zadań wybierz jedną szczegóły zadania hello tooview.

    ![Zrzut ekranu z zadania przeglądarki, z jednym z wyróżnionym zadania hello](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    wyświetlane informacje Hello jest podobne toowhat, który zostanie wyświetlony po uruchomieniu zapytania Hive i Pig, w tym linki tooview hello danych wyjściowych dziennika informacje i.

3. Można również zmodyfikować i ponownie prześlij zadanie hello w tym miejscu.

## <a name="view-hive-databases"></a>Wyświetl Hive baz danych

1. W **Eksploratora serwera**, rozwiń węzeł hello **lokalnego klastra usługi HDInsight** wpis, a następnie rozwiń węzeł **bazy danych programu Hive**. Witaj **domyślne** i **xademo** baz danych w klastrze lokalnym hello są wyświetlane. Rozszerzanie bazy danych zawiera tabele hello w hello bazy danych.

    ![Zrzut ekranu Eksploratora serwera z bazami danych rozwinięty](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Rozszerzanie tabeli Wyświetla hello kolumn dla tabeli. dane hello widoku tooquickly, kliknij prawym przyciskiem myszy tabelę, a następnie wybierz **Wyświetl pierwszych 100 wierszy**.

    ![Zrzut ekranu z Eksploratora serwera, z tabeli rozwinięty i Wyświetl pierwszych 100 wierszy wybrane](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Właściwości bazy danych i tabeli

Można wyświetlić właściwości hello bazy danych lub tabeli. Wybieranie **właściwości** Wyświetla szczegóły elementu hello wybrany w oknie właściwości hello. Na przykład zobacz hello informacje wyświetlane na powitania po zrzut ekranu:

![Zrzut ekranu właściwości okna](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Tworzenie tabeli

toocreate tabelę, kliknij prawym przyciskiem myszy bazę danych, a następnie wybierz **Create Table**.

![Zrzut ekranu z Eksploratora serwera, z Create Table wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Następnie można utworzyć tabeli hello za pomocą formularza. U dołu hello hello następującego zrzutu ekranu, zobacz hello HiveQL raw, używany toocreate hello tabela.

![Zrzut ekranu przedstawiający hello formularz używany toocreate tabeli](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Następne kroki

* [Learning liny hello hello Hortonworks piaskownicy](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Samouczek Hadoop — wprowadzenie HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
