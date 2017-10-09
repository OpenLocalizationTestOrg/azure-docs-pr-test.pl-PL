---
title: "zdarzenia aaaCorrelate w zależności od platformy Storm oraz bazy danych HBase w usłudze HDInsight"
description: "Dowiedz się, jak zdarzenia toocorrelate, pojawiające się w różnych momentach za pomocą Storm i bazy danych HBase w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Korelowanie zdarzeń pojawiające się w różnych momentach za pomocą Storm i bazy danych HBase

Przy użyciu magazynu danych z systemu Apache Storm, może skorelować danych wpisów, pojawiające się w różnych godzinach. Na przykład łączenie zdarzenia logowania i wylogowania dla toocalculate sesji użytkownika jak długo hello sesji trwała.

W tym dokumencie omówiono sposób toocreate podstawowe topologii Storm C#, który śledzi zdarzenia logowania i wylogowywania sesji użytkownika, a następnie oblicza hello czas trwania sesji hello. Topologia Hello używa bazy danych HBase jako magazynu danych. Baza danych HBase można też tooperform partii zapytań na powitania danych historycznych tooproduce dodatkowe informacje szczegółowe. Na przykład jak wiele sesji użytkownika zostały rozpoczął się lub zakończył się w określonym czasie.

## <a name="prerequisites"></a>Wymagania wstępne

* Visual Studio i hello HDInsight tools for Visual Studio. Aby uzyskać więcej informacji, zobacz [rozpocząć korzystanie z hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Apache Storm w usłudze HDInsight klastra (z systemem Windows).

  > [!WARNING]
  > Topologie SCP.NET są obsługiwane w klastrach opartych na systemie Linux Storm utworzone po 10/28/2016, hello HBase zestawu SDK pakietu .NET jest dostępny od 10/28/2016 nie działa poprawnie na HDInsight opartych na systemie Linux

* Bazy danych Apache HBase w klastrze usługi HDInsight (Linux lub z systemem Windows).

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* [Java](https://java.com) 1.7 lub nowszej na środowiska deweloperskiego. Java jest topologii hello toopackage używane, gdy jest toohello przesyłanego klastra usługi HDInsight.

  * Witaj **JAVA_HOME** środowiska zmiennej musi toohello punktu katalog, który zawiera Java.
  * Witaj **%JAVA_HOME%/bin** katalog musi znajdować się w ścieżce hello

## <a name="architecture"></a>Architektura

![Diagram przepływu danych hello za pośrednictwem hello topologii](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Korelowanie zdarzeń wymaga identyfikator wspólnej dla hello źródła zdarzenia. For example identyfikator użytkownika, identyfikator sesji lub inny element danych to) unikatowy i (b) objęte wszystkie dane przesyłane tooStorm. W tym przykładzie użyto toorepresent wartość identyfikatora GUID identyfikator sesji.

W tym przykładzie składa się z dwóch klastrów usługi HDInsight:

* HBase: dane historyczne w magazynie danych trwałych
* STORM: dane przychodzące tooingest używane

dane Hello jest generowany losowo hello topologii Storm i składa się z hello następujące elementy:

* Identyfikator sesji: identyfikator GUID, który unikatowo identyfikuje każdej sesji
* Zdarzenie: POCZĄTKOWY lub końcowy zdarzeniem. Na przykład, START zawsze występuje przed zakończeniem
* Czas: czas hello hello zdarzenia.

Te dane są przetwarzane i przechowywane w bazie danych HBase.

### <a name="storm-topology"></a>Topologii STORM

Po uruchomieniu sesji **START** zdarzeń jest odbierany przez hello topologii i rejestrowane tooHBase. Gdy **zakończenia** odebraniu zdarzenia, topologii hello pobiera hello **START** zdarzeń i oblicza hello czasu między zdarzeniami hello dwa. To **czas trwania** wartość następnie jest przechowywana w bazie danych HBase oraz hello **zakończenia** informacji o zdarzeniu.

> [!IMPORTANT]
> Gdy ta topologia przedstawia podstawowy wzorzec hello, rozwiązanie produkcji wymagałoby tootake projektu dla hello następujące scenariusze:
>
> * Zdarzeń przybywających poza kolejnością
> * Zduplikowane zdarzenia
> * Porzuconych zdarzeń

Witaj przykładowa topologia składa się z hello następujące składniki:

* Session.CS: symuluje sesji użytkownika, tworząc Identyfikatora sesji losowe okresu sesji hello czas i czas rozpoczęcia.

* Spout.CS: tworzy 100 sesji, emituje zdarzenia URUCHAMIANIA czeka hello losowe limitu czasu dla każdej sesji i następnie emituje zdarzenia zakończenia. Następnie odtwarza zakończenia sesji toogenerate nowe.

* HBaseLookupBolt.cs: używa toolook identyfikator sesji hello sesji informacji z bazy danych HBase. Podczas przetwarzania zdarzenia zakończenia znajduje hello odpowiednie zdarzenie START i oblicza hello czas trwania sesji hello.

* HBaseBolt.cs: Przechowuje informacje do bazy danych HBase.

* TypeHelper.cs: Konwersja typów odczytu / zapisu tooHBase ułatwia.

### <a name="hbase-schema"></a>Schemat bazy danych HBase

W bazie danych HBase hello dane są przechowywane w tabeli z powitania po schemat i ustawień:

* Klucz wiersza: hello sesji identyfikator jest używany jako klucz hello wiersze w tej tabeli.

* Rodziny kolumn: Nazwa rodziny hello jest "cf". Są przechowywane w tej rodzinie kolumn:

  * Zdarzenie: POCZĄTKOWY lub końcowy.

  * czas: Wystąpił hello czasu w milisekundach hello zdarzeń.

  * czas trwania: hello długość od rozpoczęcia i zakończenia zdarzenia.

* WERSJE: rodziny "cf" hello ustawiono tooretain 5 wersje każdego wiersza.

  > [!NOTE]
  > Wersje są dziennik z poprzedniej wartości przechowywanych dla klucza określonego wiersza. Domyślnie HBase tylko zwraca wartość hello hello najnowszej wersji wiersza. W takim przypadku hello tego samego wiersza jest używany dla każdej wersji wiersza jest identyfikowany przez wartość sygnatury czasowej hello wszystkie zdarzenia (START, koniec.). Wersje zapewniają widok historycznych danych dotyczących zdarzenia zarejestrowane dla określonego identyfikatora.

## <a name="download-hello-project"></a>Pobierz hello projektu

Witaj przykładowy projekt można pobrać z [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Ten plik do pobrania zawiera hello następujących projektów C#:

* CorrelationTopology: Topologii Storm C# losowo emituje zdarzenia rozpoczęcia i zakończenia sesji użytkownika. Każdej sesji ważny od 1 do 5 minut.

* SessionInfo: C# aplikacja konsolowa, która tworzy hello tabeli HBase i zawiera przykładowe zapytania tooreturn informacji o sesji przechowywanych danych.

## <a name="create-hello-table"></a>Utwórz tabelę hello

1. Otwórz hello **SessionInfo** projektu programu Visual Studio.

2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **SessionInfo** projekt i wybierz **właściwości**.

    ![Zrzut ekranu przedstawiający menu z wybrane właściwości](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Wybierz **ustawienia**, a następnie hello ustaw następujące wartości:

   * HBaseClusterURL: tooyour klaster HBase hello adresu URL. Na przykład https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: konto użytkownika hello admin/HTTP dla klastra

   * HBaseClusterPassword: hello hasła dla konta użytkownika administracyjnego/HTTP hello

   * HBaseTableName: Nazwa hello hello toouse tabeli z tego przykładu

   * HBaseTableColumnFamily: Nazwa rodziny kolumny hello

     ![Obraz okna dialogowego Ustawienia](./media/hdinsight-storm-correlation-topology/settings.png)

4. Uruchamianie hello rozwiązania. Po wyświetleniu monitu wybierz hello "c" klucza toocreate hello tabeli na klaster HBase.

## <a name="build-and-deploy-hello-storm-topology"></a>Tworzenie i wdrażanie topologii Storm hello

1. Otwórz hello **CorrelationTopology** rozwiązań w programie Visual Studio.

2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **CorrelationTopology** projektu i wybierz polecenie Właściwości.

3. W oknie właściwości hello wybierz **ustawienia** , a następnie wprowadź wartości konfiguracji powitania dla tego projektu. Witaj 5 pierwszych są hello używać tej samej wartości hello **SessionInfo** projektu:

   * HBaseClusterURL: tooyour klaster HBase hello adresu URL. Na przykład https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: hello admin/HTTP konta użytkownika dla klastra.

   * HBaseClusterPassword: hello hasło dla konta użytkownika administracyjnego/HTTP hello.

   * HBaseTableName: Nazwa hello hello toouse tabeli z tym przykładem. Ta wartość jest hello takie same nazwy tabeli, ponieważ używany w projekcie SessionInfo hello.

   * HBaseTableColumnFamily: Nazwa rodziny hello kolumny. Ta wartość jest hello takie same nazwy rodziny kolumny w hello SessionInfo projektu.

   > [!IMPORTANT]
   > Nie zmieniaj hello HBaseTableColumnNames, jako ustawienia domyślne hello są nazwy hello są używane przez **SessionInfo** tooretrieve danych.

4. Zapisz właściwości hello, a następnie kompilacji hello projektu.

5. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia hello subskrypcji platformy Azure.

   ![Obraz powitania Prześlij toostorm element menu](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. W hello **przesyłania topologii** okno dialogowe, ma toodeploy tej topologii do klastra Storm hello wybierz.

   > [!NOTE]
   > Witaj przesyłania topologii, po raz pierwszy może potrwać kilka sekund tooretrieve nazwę hello klastrów usługi HDInsight.

7. Po topologii hello toohello przekazywać i przesyłanego klastra, hello **widoku topologii Storm** otwiera i wyświetla hello systemem topologii. toorefresh hello danych, wybierz opcję hello **CorrelationTopology** i użyj przycisku Odśwież hello na powitania z góry po prawej stronie powitania.

   ![Obraz powitania topologii widoku](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Po rozpoczęciu topologii hello generowania danych hello wartość hello **Emitted** zwiększa kolumny.

   > [!NOTE]
   > Jeśli hello **widoku topologii Storm** nie jest otwierany automatycznie, użyj hello następujących tooopen kroki:
   >
   > 1. W **Eksploratora rozwiązań**, rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.
   > 2. Klaster Storm powitania kliknij prawym przyciskiem myszy hello topologii uruchomionych na, a następnie wybierz **topologii Storm widoku**

## <a name="query-hello-data"></a>Dane hello zapytania

Po wysyłanego danych użyj hello następujące kroki tooquery hello danych.

1. Zwraca toohello **SessionInfo** projektu. Jeśli nie jest uruchomiona, Uruchom nowe wystąpienie.

2. Po wyświetleniu monitu wybierz **s** toosearch rozpoczęcia zdarzenia. Są tooenter zostanie wyświetlony monit o rozpoczęcia i zakończenia czasu toodefine zakres czasu - zwracane są tylko zdarzenia między tymi dwiema wartościami godziny.

    Użyj następujących hello formatowania podczas wprowadzania hello rozpoczęcia i zakończenia razy: GG: mm i "Używam" lub "pm". Na przykład 23:20:00.

    tooreturn rejestrowane zdarzenia, użyj czas rozpoczęcia z przed hello wdrożonej topologii Storm i czas zakończenia teraz. Witaj zwracanych danych zawiera wpisy toohello podobne następującego tekstu:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Wyszukiwanie zakończenia zdarzenia działa hello sam jako rozpoczęcia zdarzenia. Jednak zakończenia zdarzenia są generowane losowo od 1 do 5 minut po hello rozpoczęcia zdarzenia. Tootry może mieć kilka zakresów toofind hello zakończenia zdarzenia w czasie. Zdarzenia zakończenia zawierają również hello czas trwania sesji hello - hello różnica między hello rozpoczęcia zdarzenia czas i czas zakończenia zdarzenia. Oto przykładowe dane dla zdarzenia zakończenia:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Wartości czasu hello są według czasu lokalnego, czas hello zwracane z kwerendy hello jest w formacie UTC.

## <a name="stop-hello-topology"></a>Zatrzymywanie topologii hello

Gdy wszystko jest gotowe toostop hello topologii, zwróć toohello **CorrelationTopology** projektu programu Visual Studio. W hello **widoku topologii Storm**, wybierz hello topologii, a następnie użyj hello **Kill** u góry hello hello topologii widoku.

## <a name="delete-your-cluster"></a>Usuwanie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej przykładów Storm, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).
