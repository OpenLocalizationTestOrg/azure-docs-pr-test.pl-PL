---
title: "aaaUse Ambari Tez widoku z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse Ambari Tez wyświetlić toodebug Tez zadania w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Użyj widoków Ambari toodebug Tez zadania w usłudze HDInsight

Witaj Interfejsu sieci Web Ambari dla usługi HDInsight zawiera widok Tez, które mogą być używane toounderstand i debugowania zadania, które korzystają z aplikacji Tez. Widok Tez Hello umożliwia toovisualize hello zadania jako wykres połączonych elementów, przejdź do każdego elementu, a następnie pobrać statystyk i informacje o rejestrowaniu.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster usługi HDInsight opartej na systemie Linux. Aby uzyskać instrukcje dotyczące tworzenia klastra, zobacz [rozpocząć korzystanie z usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Nowoczesna przeglądarka sieci Web, obsługująca język HTML5.

## <a name="understanding-tez"></a>Opis aplikacji Tez

Tez jest rozszerzalną strukturą do przetwarzania danych w Hadoop, która zapewnia większe szybkości niż tradycyjne przetwarzania MapReduce. W przypadku klastrów usługi HDInsight opartej na systemie Linux jest hello domyślny aparat gałęzi.

Tez tworzy skierowane acykliczne wykresu (DAG) opisujący hello kolejność akcji wymaganych przez zadania. Poszczególne działania są nazywane wierzchołki i wykonać fragment hello ogólną zadania. Hello rzeczywistego wykonania pracy hello opisanego przez wierzchołek nosi nazwę zadania i mogą być rozproszone na wielu węzłach w klastrze hello.

### <a name="understanding-hello-tez-view"></a>Opis hello widoku aplikacji Tez

Witaj Tez widok zawiera zarówno historyczne informacje i po procesów, które są uruchomione. Te informacje pokazują, jak zadanie jest dystrybuowana do klastrów. Wyświetlane są również używane przez zadania i wierzchołków liczników i toohello zadania powiązane informacje o błędzie. Może on oferować przydatnych informacji w hello następujące scenariusze:

* Monitorowanie procesy długotrwałe, wyświetlanie hello postęp mapowania i zmniejszyć zadania.
* Analizowanie dane historyczne dotyczące toolearn procesów powiodły się czy nie, jak można poprawić przetwarzania lub przyczyny niepowodzenia.

## <a name="generate-a-dag"></a>Generowanie DAG

Hello Tez widok zawiera dane tylko jeśli zadanie, które używa hello Tez aparat jest obecnie uruchomiony lub wcześniej uruchomione. Proste zapytań programu Hive można rozpoznawać bez korzystania z aplikacji Tez. Bardziej złożone kwerendy tego czy filtrowanie, grupowanie, kolejność, sprzężenia, itp. Użyj hello Tez aparatu.

Użyj hello następujące kroki toorun zapytań programu Hive, która używa Tez:

1. W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą hello klastra usługi HDInsight.

2. Witaj menu u góry hello hello strony i wybierz polecenie hello **widoków** ikony. Ta ikona wygląda jak seria kwadratów. Hello listy rozwijanej, która jest wyświetlana, wybierz **Hive widoku**.

    ![Wybranie widoku Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Witaj widoku Hive załadowanie, Wklej hello następujące zapytanie w hello edytora zapytań, a następnie kliknij **wykonania**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Po zakończeniu zadania hello powinny być widoczne dane wyjściowe hello wyświetlane w hello **wyniki przetwarzania zapytania** sekcji. Witaj wyniki powinny być podobne toohello następującego tekstu:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Wybierz hello **dziennika** kartę. Zostaną wyświetlone informacje toohello podobne następującego tekstu:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Zapisz hello **identyfikator aplikacji** wartość, jak ta wartość jest używana w następnej sekcji hello.

## <a name="use-hello-tez-view"></a>Użyj hello widoku aplikacji Tez

1. Witaj menu u góry hello hello strony i wybierz polecenie hello **widoków** ikony. Hello listy rozwijanej, która jest wyświetlana, wybierz **widoku Tez**.

    ![Wybranie widoku aplikacji Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Podczas ładowania hello widoku Tez widać listę zapytań hive, które są aktualnie uruchomione lub zostały uruchomione w klastrze hello.

    ![Wszystkie grupy DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Jeśli masz tylko jeden wpis dotyczy zapytanie hello, uruchomionego w poprzedniej sekcji hello. Jeśli masz wiele wpisów można wyszukiwać za pomocą pola hello u góry hello hello strony.

4. Wybierz hello **identyfikator zapytania** dla zapytania programu Hive. Informacje o kwerendzie hello jest wyświetlany.

    ![Szczegóły grupy DAG.](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. karty Hello na tej stronie umożliwiają hello tooview następujących informacji:

    * **Zapytanie szczegóły**: szczegółowe informacje o hello zapytania Hive.
    * **Oś czasu**: dowiedzieć się, jak długo trwało każdego etapu przetwarzania.
    * **Konfiguracje**: hello konfiguracji używane dla tego zapytania.

    Z __szczegóły kwerendy__ można użyć hello łącza toofind informacji na temat hello __aplikacji__ lub hello __DAG__ dla tego zapytania.
    
    * Witaj __aplikacji__ łącze Wyświetla informacje o hello YARN aplikacji dla tego zapytania. W tym miejscu można uzyskać dostępu do dzienników aplikacji hello YARN.
    * Witaj __DAG__ łącze Wyświetla informacje o hello ukierunkowanego wykresu acyklicznego. dla tego zapytania. W tym miejscu można wyświetlić graficzną reprezentację hello grupy DAG. Można również znaleźć informacji o hello wierzchołków w hello grupy DAG.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy wiesz już, jak wyświetlić toouse hello Tez, Dowiedz się więcej o [przy użyciu Hive w usłudze HDInsight](hdinsight-use-hive.md).

Aby uzyskać szczegółowe informacje techniczne na temat aplikacji Tez, zobacz hello [Tez strony o Hortonworks](http://hortonworks.com/hadoop/tez/).

Aby uzyskać więcej informacji na temat używania narzędzia Ambari z usługą HDInsight, zobacz [Zarządzanie klastrów usługi HDInsight przy użyciu hello Interfejsu sieci Web Ambari](hdinsight-hadoop-manage-ambari.md)
