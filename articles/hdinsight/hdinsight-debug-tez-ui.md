---
title: "aaaUse interfejsu użytkownika aplikacji Tez z usługą HDInsight opartych na systemie Windows - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse toodebug interfejsu użytkownika aplikacji Tez Tez zadania w usłudze HDInsight HDInsight dla systemu Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Użyj hello interfejsu użytkownika aplikacji Tez toodebug Tez zadania w usłudze HDInsight z systemu Windows
Witaj Tez interfejsu użytkownika jest strony sieci web, które mogą być używane toounderstand i debugowanie zadań, korzystających z aplikacji Tez jako aparat wykonywania hello w klastrach HDInsight opartych na systemie Windows. Hello interfejsu użytkownika aplikacji Tez umożliwia toovisualize hello zadania jako wykres połączonych elementów, przejdź do każdego elementu, a następnie pobrać statystyk i informacje o rejestrowaniu.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight z systemem Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="prerequisites"></a>Wymagania wstępne
* Klaster usługi HDInsight opartej na systemie Windows. Aby uzyskać instrukcje dotyczące tworzenia nowego klastra, zobacz [rozpocząć korzystanie z usługi HDInsight opartej na systemie Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Hello Tez interfejsu użytkownika jest dostępna tylko w klastrach HDInsight opartych na systemie Windows utworzone po 8 lutego 2016 r.
  >
  >
* Klient pulpitu zdalnego z systemem Windows.

## <a name="understanding-tez"></a>Opis aplikacji Tez
Tez jest rozszerzalną strukturą do przetwarzania danych w Hadoop, która zapewnia większe szybkości niż tradycyjne przetwarzania MapReduce. W przypadku klastrów usługi HDInsight opartej na systemie Windows jest opcjonalny mechanizm, który można włączyć dla gałęzi przy użyciu następującego polecenia w ramach zapytania Hive hello:

    set hive.execution.engine=tez;

Podczas pracy jest tooTez przesłane, tworzy skierowane acykliczne Graph (DAG) opisujący hello kolejność wykonywania działań hello wymagane przez zadanie hello. Poszczególne działania są nazywane wierzchołki i wykonać fragment hello ogólną zadania. Hello rzeczywistego wykonania pracy hello opisanego przez wierzchołek nosi nazwę zadania i mogą być rozproszone na wielu węzłach w klastrze hello.

### <a name="understanding-hello-tez-ui"></a>Opis hello Tez interfejsu użytkownika
strony sieci web zapewnia informacji na temat procesów, które są uruchomione lub mieć wcześniej został uruchomiony przy użyciu aplikacji Tez jest Hello Tez interfejsu użytkownika. Umożliwia hello tooview DAG wygenerowane w aplikacji Tez, liczniki jak dystrybuowana klastrów, takie jak pamięć używane przez zadania i wierzchołki i informacje o błędzie. Może on oferować przydatnych informacji w hello następujące scenariusze:

* Monitorowanie procesy długotrwałe, wyświetlanie hello postęp mapowania i zmniejszyć zadania.
* Analizowanie dane historyczne dotyczące toolearn procesów powiodły się czy nie, jak można poprawić przetwarzania lub przyczyny niepowodzenia.

## <a name="generate-a-dag"></a>Generowanie DAG
Jeśli zadanie, które używa hello Tez aparat jest aktualnie uruchomione lub zostało uruchomione w ostatnich hello Hello interfejsu użytkownika aplikacji Tez tylko zawierają dane. Proste zapytań programu Hive można rozpoznawać zwykle bez korzystania z aplikacji Tez, jednak bardziej złożonych zapytań, które wykonaj filtrowanie, grupowanie, kolejność sprzężenia, itp. zwykle wymagają Tez.

Użyj hello następujące kroki toorun zapytań programu Hive, które będą wykonywane przy użyciu aplikacji Tez.

1. W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą hello klastra usługi HDInsight.
2. Witaj menu u góry hello hello strony i wybierz polecenie hello **Edytor Hive**. Spowoduje to wyświetlenie strony z hello następujące przykładowe zapytanie.

        Select * from hivesampletable

    ERASE hello przykładowe zapytanie i zastąp go hello poniżej.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Wybierz hello **przesyłania** przycisku. Witaj **sesji zadania** sekcji u dołu strony hello hello jest wyświetlany stan hello hello zapytania. Raz zbyt hello zmiany stanu**Ukończono**, wybierz pozycję hello **Wyświetl szczegóły** link tooview hello wyników. Witaj **dane wyjściowe zadania** powinny być podobne toohello następujące czynności:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Użyj hello Tez interfejsu użytkownika
> [!NOTE]
> Hello Tez interfejsu użytkownika jest dostępna wyłącznie z pulpitem hello hello głównymi węzłami klastra, trzeba używać węzłów głównych toohello tooconnect pulpitu zdalnego.
>
>

1. Z hello [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight. Z góry hello hello HDInsight bloku, wybierz hello **pulpitu zdalnego** ikony. Spowoduje to wyświetlenie bloku pulpitu zdalnego hello

    ![Ikony pulpitu zdalnego](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. W bloku pulpitu zdalnego hello, wybierz **Connect** węzła głównego klastra toohello tooconnect. Po wyświetleniu monitu użyj hello klastra Podłączanie pulpitu zdalnego użytkownika nazwę i hasło tooauthenticate hello.

    ![Ikona połączenia pulpitu zdalnego](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Jeśli połączenie pulpitu zdalnego nie jest włączone, wprowadź nazwę użytkownika, hasło oraz Data wygaśnięcia, a następnie wybierz **włączyć** tooenable pulpitu zdalnego. Po jej włączeniu, użyj hello poprzednich kroków tooconnect.
   >
   >
3. Po nawiązaniu połączenia, Otwórz program Internet Explorer na powitania pulpitu zdalnego, wybierz hello koło zębate ikonę w hello górnym rogu przeglądarki hello, a następnie wybierz **ustawienia widoku zgodności**.
4. Od dołu hello **ustawienia widoku zgodności**, wyczyść pola wyboru hello **wyświetlić witryn intranetowych w widoku zgodności** i **listy zgodności użycia programu Microsoft**, a następnie wybierz **Zamknij**.
5. W programie Internet Explorer przejdź toohttp://headnodehost:8188/tezui / #/. Spowoduje to wyświetlenie hello Tez interfejsu użytkownika

    ![Interfejs użytkownika aplikacji tez](./media/hdinsight-debug-tez-ui/tezui.png)

    Po załadowaniu hello Tez interfejsu użytkownika, pojawi się, że listy grupy DAG, które są aktualnie uruchomione lub zostały uruchomione na powitania klastra. Widok domyślny Hello obejmuje hello Nazwa grupy Dag, identyfikator przesyłający, stan, czas rozpoczęcia, godziny zakończenia, czas trwania, identyfikator aplikacji i kolejki. Przy użyciu hello koło zębate ikonę na powitania po prawej strony hello można dodać więcej kolumn.

    Jeśli masz tylko jeden wpis będzie dla zapytania hello, uruchomionego w poprzedniej sekcji hello. Jeśli masz wiele wpisów, można wyszukać, wpisując kryteria wyszukiwania w polach hello powyżej hello grupy DAG, a następnie kliknij przycisk **Enter**.
6. Wybierz hello **Nazwa grupy Dag** hello najnowszych DAG wpisu. Spowoduje to wyświetlenie informacji o hello DAG, a także toodownload opcji hello zip pliki w formacie JSON, które zawierają informacje dotyczące hello DAG.

    ![Szczegóły grupy DAG.](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Powyżej hello **szczegóły DAG** są kilka łącza, które mogą być używane toodisplay informacji na temat hello grupy DAG.

   * **Liczniki DAG** Wyświetla liczniki informacje dla tej grupy DAG.
   * **Widok graficzny** Wyświetla graficzną reprezentację tej grupy DAG.
   * **Wszystkich wierzchołków** zostanie wyświetlona lista hello wierzchołków w tej grupy DAG.
   * **Wszystkie zadania** zostanie wyświetlona lista hello zadania dla wszystkich wierzchołków w tej grupy DAG.
   * **Wszystkie TaskAttempts** Wyświetla informacje o hello prób toorun zadań dla tej grupy DAG.

     > [!NOTE]
     > Podczas przewijania hello kolumny wyświetlanej wierzchołków, zadania i TaskAttempts, zwróć uwagę, że istnieją łączy tooview **liczniki** i **wyświetlić lub pobrać dzienniki** dla każdego wiersza.
     >
     >

     Jeśli wystąpił błąd z zadaniem hello, hello DAG szczegółów będzie wyświetlany stan nie powiodła się, wraz z tooinformation łącza o hello zadania nie powiodło się. Informacje diagnostyczne pojawi się poniżej szczegóły hello grupy DAG.
8. Wybierz **widoku graficznego**. Spowoduje to wyświetlenie graficzną reprezentację hello grupy DAG. Można umieścić hello myszy przez każdy wierzchołek hello widoku toodisplay informacje o nim.

    ![Widok graficzny](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Kliknięcie wierzchołek załaduje hello **szczegóły wierzchołków** dla tego elementu. Polecenie hello **1 mapy** wierzchołków toodisplay szczegóły dla tego elementu. Wybierz **Potwierdź** tooconfirm hello nawigacji.

    ![Szczegóły wierzchołków](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Należy zauważyć, że możesz teraz łącza u góry hello hello strony, które są powiązane toovertices i zadania.

    > [!NOTE]
    > Tej strony można również przyjeździe, przechodząc zbyt**szczegóły DAG**, wybierając żądane **szczegóły wierzchołków**i wybierając hello **1 mapy** wierzchołka.
    >
    >

    * **Liczniki wierzchołków** Wyświetla informacje o liczniku tym wierzchołka.
    * **Zadania** Wyświetla zadania dla tego wierzchołka.
    * **Zadanie prób** Wyświetla informacje o zadaniach toorun prób dla tego wierzchołka.
    * **Źródłem & wychwytywanie** wyświetla źródła danych i sink tego wierzchołka.

      > [!NOTE]
      > Z menu poprzedniej hello podczas przewijania hello kolumny wyświetlanej dla zadań, toodisplay prób zadań i źródeł & Sinks__ łączy toomore informacje dla każdego elementu.
      >
      >
11. Wybierz **zadania**, a następnie wybierz hello elementu o nazwie **00_000000**. Spowoduje to wyświetlenie **szczegóły zadania** dla tego zadania. Na tym ekranie można wyświetlić **liczniki zadań** i **zadań prób**.

    ![Szczegóły zadania](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Następne kroki
Teraz, gdy wiesz już, jak wyświetlić toouse hello Tez, Dowiedz się więcej o [przy użyciu Hive w usłudze HDInsight](hdinsight-use-hive.md).

Aby uzyskać szczegółowe informacje techniczne na temat aplikacji Tez, zobacz hello [Tez strony o Hortonworks](http://hortonworks.com/hadoop/tez/).
