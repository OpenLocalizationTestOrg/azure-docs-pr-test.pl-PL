---
title: "aaaQuery Hive za pośrednictwem sterownik JDBC hello - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj sterownik JDBC hello z tooHadoop zapytań Hive toosubmit Java aplikacji w usłudze HDInsight. Połącz programowo i z powitania klienta SQuirrel SQL."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Zapytanie Hive za pośrednictwem sterownik JDBC hello w usłudze HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Dowiedz się, jak sterownik JDBC hello toouse z toosubmit aplikacji Java Hive odpytuje tooHadoop w usłudze Azure HDInsight. Witaj informacje w tym dokumencie przedstawiono sposób tooconnect programowo i z hello SQuirrel klienta SQL.

Aby uzyskać więcej informacji na powitania interfejsu JDBC Hive, zobacz [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Wymagania wstępne

* Hadoop w klastrze usługi HDInsight. Praca klastrach opartych na systemie Linux albo systemem Windows.

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [wycofanie HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL jest aplikacją kliencką JDBC.

* Witaj [Java Developer Kit (JDK) w wersji 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej.

* [Apache Maven](https://maven.apache.org). Maven jest projektem systemu dla projektów języka Java, używanego przez projekt hello skojarzone z tym artykułem kompilacji.

## <a name="jdbc-connection-string"></a>Parametry połączenia sterownika JDBC

Klaster usługi HDInsight tooan JDBC połączeń na platformie Azure są wprowadzane ponad 443, a ruch hello jest zabezpieczone przy użyciu protokołu SSL. Hello publicznego bramy, która klastrów hello sit za przekierowuje hello ruchu toohello portu nasłuchiwania serwera HiveServer2 faktycznie na. Witaj poniżej znajduje się przykład parametry połączenia:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Zastąp `CLUSTERNAME` o nazwie hello klastra usługi HDInsight.

## <a name="authentication"></a>Authentication

Podczas ustanawiania połączenia hello, musisz użyć hello HDInsight klastra Administrator nazwy i hasła tooauthenticate toohello klastra bramy. Podczas nawiązywania połączenia z klientami JDBC, takich jak SQuirreL SQL, wprowadź hello admin nazwy i hasła w ustawieniach klienta.

Z poziomu aplikacji Java musi używać hello nazwy i hasła podczas ustanawiania połączenia. Na przykład hello następujący kod w języku Java otwiera nowe połączenie przy użyciu parametrów połączenia hello, nazwę administratora i hasła:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Połączenie z klientem SQuirreL SQL

SQuirreL SQL jest klientem JDBC, które mogą być używane tooremotely uruchamiania zapytań Hive z klastrem usługi HDInsight. Witaj następujących krokach założono zainstalowano SQuirreL SQL.

1. Skopiuj hello Hive JDBC sterowniki z klastrem usługi HDInsight.

    * Dla **HDInsight opartych na systemie Linux**, użyj następujących hello kroki pliki jar hello wymagane toodownload.

        1. Utwórz katalog zawierający pliki hello. Na przykład `mkdir hivedriver`.

        2. Z wiersza polecenia użyj następujących hello polecenia toocopy hello plików z klastrem usługi HDInsight hello:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Zastąp `USERNAME` z nazwą konta użytkownika SSH hello hello klastra. Zastąp `CLUSTERNAME` o nazwie klastra usługi HDInsight hello.

    * Dla **HDInsight opartych na systemie Windows**, użyj następujących hello kroki pliki jar hello toodownload.

        1. Z hello portalu Azure, wybierz z klastrem usługi HDInsight, a następnie wybierz hello **pulpitu zdalnego** ikony.

            ![Ikony pulpitu zdalnego](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. W bloku hello pulpitu zdalnego za pomocą hello **Connect** przycisk tooconnect toohello klastra. Jeśli hello pulpitu zdalnego nie jest włączona, użyj hello formularza tooprovide nazwę użytkownika i hasło, a następnie wybierz **włączyć** tooenable pulpitu zdalnego dla klastra hello.

            ![Blok pulpitu zdalnego](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Po wybraniu **Connect**, zostanie pobrany plik RDP. Korzystając z tego pliku toolaunch hello pulpitu zdalnego klienta. Po wyświetleniu monitu użyj hello nazwę użytkownika i hasło dostępu do pulpitu zdalnego.

        3. Po nawiązaniu połączenia, skopiuj następujące pliki z komputera lokalnego tooyour sesji pulpitu zdalnego hello hello. Umieść je w lokalnym katalogu o nazwie `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-Standalone.JAR
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.JAR
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.JAR

            > [!NOTE]
            > Witaj w wersji numery objęte hello ścieżki i nazwy plików mogą być inne dla klastra.

        4. Rozłączenie sesji pulpitu zdalnego powitania po zakończeniu kopiowania plików hello.

2. Uruchom aplikację SQuirreL SQL hello. Od lewej hello hello okna, wybierz **sterowniki**.

    ![Sterowniki karty po lewej stronie powitania hello okna](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Z ikon hello u góry hello hello **sterowniki** okno dialogowe, wybierz opcję hello  **+**  toocreate ikona sterownika.

    ![Ikony sterowniki](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. W oknie dialogowym Dodawanie sterownika hello Dodaj hello następujących informacji:

    * **Nazwa**: Hive
    * **Przykładowy adres URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Dodatkowe ścieżki klasy**: Użyj hello Dodaj przycisk tooadd hello jar pliki pobrane wcześniej
    * **Nazwa klasy**: org.apache.hive.jdbc.HiveDriver

   ![Dodaj sterownik okna dialogowego](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Kliknij przycisk **OK** toosave te ustawienia.

5. Powitania po lewej stronie okna SQuirreL SQL hello wybierz **aliasy**. Następnie kliknij przycisk hello  **+**  toocreate ikona alias połączenia.

    ![Dodaj nowy alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Użyj następujących hello wartości hello **Dodaj Alias** okna dialogowego.

    * **Nazwa**: Hive w usłudze HDInsight

    * **Sterownik**: Użyj hello listy rozwijanej tooselect hello **Hive** sterownika

    * **Adres URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.

    * **Nazwa użytkownika**: Nazwa konta logowania hello klastra dla klastra usługi HDInsight. Domyślnie Hello `admin`.

    * **Hasło**: hello hasła konta logowania hello klastra.

 ![Dodaj alias okna dialogowego](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Użyj hello **testu** tooverify przycisku, który hello połączenie działa. Gdy **nawiązać: Hive w usłudze HDInsight** zostanie wyświetlone okno dialogowe, wybierz **Connect** tooperform hello testu. Jeśli hello test zakończy się pomyślnie, zostanie wyświetlony **połączenie przebiegło pomyślnie** okna dialogowego.

    połączenie hello toosave alias, użyj hello **Ok** u dołu hello hello **Dodaj Alias** okna dialogowego.

7. Z hello **nawiązać** wybierz z listy rozwijanej na górze hello SQuirreL SQL **Hive w usłudze HDInsight**. Po wyświetleniu monitu wybierz **Connect**.

    ![w oknie dialogowym połączenia](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Po nawiązaniu połączenia, wprowadź hello następujące zapytanie do okna dialogowego zapytania SQL hello, a następnie wybierz hello **Uruchom** ikony. obszar wyników Hello powinny być wyświetlane hello wyniki zapytania hello.

        select * from hivesampletable limit 10;

    ![okno dialogowe kwerendy SQL, łącznie z wynikami](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Połącz się z przykładem aplikacji Java

Przykład użycia tooquery klienta Java Hive w usłudze HDInsight jest dostępna w [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Wykonaj te instrukcje hello hello toobuild repozytorium, a następnie uruchom przykładowe hello.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Wystąpił nieoczekiwany błąd podczas próby tooopen połączenia SQL

**Objawy**: podczas łączenia z klastrem usługi HDInsight tooan, który jest w wersji 3.3 lub 3.4, może zostać wyświetlony błąd, który wystąpił nieoczekiwany błąd. Witaj śladu stosu dla tego błędu rozpoczyna się od hello następujące wiersze:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Przyczyna**: niezgodność wersji hello pliku commons codec.jar hello używanego przez SQuirreL i hello wymagana przez składniki Hive JDBC hello przyczyną tego błędu.

**Rozdzielczość**: toofix tego błędu, użyj hello następujące kroki:

1. Pobierz plik jar koder-dekoder commons hello z klastrem usługi HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Zakończ SQuirreL, a następnie przejdź katalogu toohello zainstalowanym SQuirreL w tym systemie. W katalogu SquirreL hello, hello `lib` katalogu, Zastąp hello istniejących na commons codec.jar z jedną pobrane z klastrem usługi HDInsight hello hello.

3. Uruchom ponownie SQuirreL. Błąd Hello już powinien wystąpić, gdy połączenie tooHive w usłudze HDInsight.

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już jak toowork JDBC toouse przy użyciu Hive, hello Użyj następujących łączy tooexplore toowork inne sposoby z usługą Azure HDInsight.

* [Przekazywanie danych tooHDInsight](hdinsight-upload-data.md)
* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystanie z zadań MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)
