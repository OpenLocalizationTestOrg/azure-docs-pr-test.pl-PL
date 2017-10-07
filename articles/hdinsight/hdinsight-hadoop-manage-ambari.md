---
title: "aaaMonitor i zarządzać nimi za pomocą interfejsu użytkownika sieci Web Ambari w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Ambari toomonitor i zarządzania klastrami usługi HDInsight opartej na systemie Linux. W tym dokumencie możesz dowiedzieć się, jak klastrów hello toouse Interfejsu sieci Web Ambari dołączone do usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Zarządzanie klastrami usługi HDInsight za pomocą hello Interfejsu sieci Web Ambari

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari upraszcza hello zarządzania i monitorowania klastrów platformy Hadoop, zapewniając łatwy toouse interfejsu użytkownika i REST interfejsu API sieci web. Ambari znajduje się w klastrach HDInsight opartych na systemie Linux i jest używane toomonitor hello klastra i dokonywać zmian konfiguracji.

W tym dokumencie możesz dowiedzieć się, jak toouse hello Interfejsu sieci Web Ambari z klastrem usługi HDInsight.

## <a id="whatis"></a>Co to jest Ambari?

[Apache Ambari](http://ambari.apache.org) ułatwia zarządzanie Hadoop, zapewniając łatwy w użyciu interfejsu użytkownika sieci web. Można używać narzędzia Ambari tworzenia, zarządzania i monitorowania klastrów platformy Hadoop. Deweloperzy mogą integrować te możliwości w swoich aplikacjach przy użyciu hello [interfejsów API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Domyślnie z klastrami usługi HDInsight, które używają systemu operacyjnego Linux hello jest udostępniany Hello Interfejsu sieci Web Ambari.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). 

## <a name="connectivity"></a>Łączność

Hello Interfejsu sieci Web Ambari jest dostępna w klastrze usługi HDInsight w HTTPS://CLUSTERNAME.azurehdidnsight.net, gdzie **CLUSTERNAME** jest hello nazwą klastra.

> [!IMPORTANT]
> Połączenie tooAmbari w usłudze HDInsight wymaga protokołu HTTPS. Po wyświetleniu monitu na potrzeby uwierzytelniania, użyj nazwy konta administratora hello i hasło podane podczas tworzenia klastra hello.

## <a name="ssh-tunnel-proxy"></a>Tunel SSH (proxy)

Gdy Ambari dla klastra jest dostępny bezpośrednio przez hello Internet, niektóre łącza z interfejsu użytkownika sieci Web Ambari (na przykład toohello JobTracker) nie są widoczne na powitania hello internet. tooaccess tych usług, należy utworzyć tunelu SSH. Aby uzyskać więcej informacji, zobacz [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Interfejs użytkownika sieci Web Ambari

Podczas łączenia z toohello Interfejsu sieci Web Ambari, to zostanie wyświetlony monit o tooauthenticate toohello strony. Użyj użytkownika Administrator klastra hello (ustawienie domyślne Admin) i hasło użyte podczas tworzenia klastra.

Gdy zostanie otwarta strona hello, należy pamiętać, pasek hello u góry hello. Ten pasek zawiera hello następujące informacje i kontrolki:

![Nawiguj do ambari](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Logo narzędzia Ambari** -pulpit nawigacyjny hello zostanie otwarta, które mogą być używane toomonitor hello klastra.

* **Ops # nazwy klastra** -Wyświetla liczbę hello trwających operacji narzędzia Ambari. Wybieranie nazwy klastra hello lub **# ops** zostanie wyświetlona lista operacje w tle.

* **alerty #** -wyświetla ostrzeżenia lub alerty krytyczne dla hello klastra.

* **Pulpit nawigacyjny** -Wyświetla hello w pulpicie nawigacyjnym.

* **Usługi** — ustawienia informacji i konfiguracji usług hello hello klastra.

* **Hosty** -informacji i ustawień konfiguracji dla hello węzłów w klastrze hello.

* **Alerty** -dziennika informacje, ostrzeżenia i alerty krytyczne.

* **Administrator** -oprogramowania stosu/usług, które są zainstalowane w klastrze hello, informacje o koncie usługi i zabezpieczeń protokołu Kerberos.

* **Przycisk Admin** -Ambari zarządzania, ustawienia użytkownika i wylogowania.

## <a name="monitoring"></a>Monitorowanie

### <a name="alerts"></a>Alerty

Witaj Poniższa lista zawiera hello wspólnej stany alertów używana przez narzędzia Ambari:

* **OK**
* **Ostrzeżenie**
* **KRYTYCZNE**
* **NIEZNANY**

Alerty innych niż **OK** spowodować hello **alerty #** wpis u góry hello hello strony toodisplay hello liczbę alertów. Wybranie tego wpisu powoduje wyświetlenie hello alertów i ich stan.

Alerty są podzielone na kilka domyślnych grup, które mogą być wyświetlane z hello **alerty** strony.

![Strona alertów](./media/hdinsight-hadoop-manage-ambari/alerts.png)

Witaj grup można zarządzać za pomocą hello **akcje** menu i wybierając **Zarządzaj grupami alertu**.

![Zarządzanie grupami alertu w oknie dialogowym](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

Można również zarządzać metody alertów i utworzyć powiadomienia o alertach z hello **akcje** menu, wybierając __Zarządzanie powiadomienia Alert__. Bieżący powiadomienia są wyświetlane. Powiadomienia można również utworzyć w tym miejscu. Powiadomienia mogą być wysyłane za pośrednictwem **E-mail** lub **SNMP** przypadku wystąpienia określonych ważności alertu/kombinacji. Na przykład możesz wysłać wiadomość e-mail, gdy dowolne hello alertów w hello **domyślne YARN** grupy ustawiono zbyt**krytyczny**.

![Tworzenie okna dialogowego alertu](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Ponadto wybierając __Zarządzaj ustawieniami Alert__ z hello __akcje__ menu pozwala tooset hello liczba alertu musi wystąpić, aby wysłać powiadomienia. To ustawienie może być powiadomienia tooprevent używanych w przypadku błędów przejściowych.

### <a name="cluster"></a>Klaster

Witaj **metryki** kartę hello pulpit nawigacyjny zawiera szereg elementy widget, dzięki któremu można łatwo toomonitor hello stan klastra jeden rzut oka. Kilka elementów widget, takich jak **użycie procesora CPU**, znajdują się dodatkowe informacje po kliknięciu.

![pulpit nawigacyjny z metryk](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Witaj **Heatmaps** karcie są wyświetlane jako kolorowe heatmaps, z zielonym toored metryki.

![pulpit nawigacyjny z heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Aby uzyskać więcej informacji na powitania węzłów w klastrze hello wybierz **hostów**. Następnie wybierz hello określonego węzła, który chcesz.

![Szczegóły hosta](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Usługi

Witaj **usług** paska bocznego na powitania pulpit nawigacyjny zapewnia szybki wgląd w stan hello hello usługi działające na powitania klastra. Różne ikony są używane tooindicate stanu lub akcje, które należy podjąć. Na przykład symbol żółty odtworzenia jest wyświetlana, jeśli usługa musi toobe ponownego przetworzenia.

![pasek boczny usług](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> usługi Hello wyświetlane różnią się typy klastrów usługi HDInsight i wersje. usługi Hello tutaj wyświetlane mogą być inne niż usług hello wyświetlane dla klastra.

Wybranie usługi powoduje wyświetlenie bardziej szczegółowych informacji w usłudze hello.

![Podsumowanie usługi](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Szybkie łącza

Wyświetlanie niektórych usług **szybkie linki** łącze u góry hello hello strony. Może to być używane tooaccess specyficzne dla usługi web UI, takich jak:

* **Historia zadań** -historii zadań MapReduce.
* **Menedżer zasobów** -YARN ResourceManager UI.
* **NameNode** -Hadoop Distributed Interfejsu NameNode (HDFS) systemu plików.
* **Interfejs użytkownika sieci Web Oozie** -Oozie interfejsu użytkownika.

Wybranie dowolnego z tych łączy otwiera nową kartę w przeglądarce, która wyświetla hello wybranej strony.

> [!NOTE]
> Wybór hello **szybkie linki** wpis dla usługi mogą zwracać błąd "nie można odnaleźć serwera". Jeśli ten błąd wystąpi, należy użyć tunelu SSH przy użyciu hello **szybkie linki** wpis dla tej usługi. Aby uzyskać informacje, zobacz [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)

## <a name="management"></a>Zarządzanie

### <a name="ambari-users-groups-and-permissions"></a>Ambari użytkowników, grup i uprawnień

Praca z użytkownikami, grupami i uprawnienia są obsługiwane w przypadku korzystania z [przyłączony do domeny](hdinsight-domain-joined-introduction.md) klastra usługi HDInsight. Uzyskać informacji na temat używania hello interfejsu użytkownika zarządzania Ambari w klastrze przyłączonych do domeny, zobacz [zarządzania klastrami HDInsight przyłączonych do domeny](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> Nie należy zmieniać hasła hello hello Ambari strażnika (hdinsightwatchdog) w klastrze usługi HDInsight opartej na systemie Linux. Zmiana podziały hasła hello hello akcji skryptu toouse możliwości lub operacji skalowania z klastrem.

### <a name="hosts"></a>Hosts

Witaj **hostów** strona zawiera listę wszystkich hostów w klastrze hello. hosty toomanage, wykonaj następujące kroki.

![strony hosty](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> Dodawanie, wycofywanie z eksploatacji i recommissioning hosta nie można używać z klastrami usługi HDInsight.

1. Wybierz host hello, że chcesz toomanage.

2. Użyj hello **akcje** hello akcji tooselect menu, że chcesz tooperform:

   * **Uruchom wszystkie składniki** -uruchomić wszystkie składniki hello hoście.

   * **Zatrzymaj wszystkie składniki** -zatrzymania wszystkich składników na hoście hello.

   * **Uruchom ponownie wszystkie składniki** — zatrzymano i uruchomić wszystkie składniki na powitania hosta.

   * **Włącz tryb konserwacji** -pomija alerty dla hello hosta. W tym trybie powinien być włączony, jeśli przeprowadzasz akcje, które generują alerty. Na przykład zatrzymywania i uruchamiania usługi.

   * **Wyłącz tryb konserwacji** — zwraca tekst hello alerty toonormal hosta.

   * **Zatrzymaj** -zatrzymuje DataNode lub NodeManagers na hoście hello.

   * **Uruchom** — uruchamia DataNode lub NodeManagers na hoście hello.

   * **Uruchom ponownie** -przerywa działanie i uruchamia DataNode lub NodeManagers na hoście hello.

   * **Likwidowanie** — usuwa z hello klastra hosta.

     > [!NOTE]
     > Nie należy używać tej akcji w klastrach usługi HDInsight.

   * **Recommission** -dodaje toohello wcześniej zlikwidowana hosta klastra.

     > [!NOTE]
     > Nie należy używać tej akcji w klastrach usługi HDInsight.

### <a id="service"></a>Usługi

Z hello **pulpitu nawigacyjnego** lub **usług** Użyj hello **akcje** znajdujący się u dołu hello hello listę usług toostop i uruchomić wszystkie usługi.

![Akcje usługi](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Gdy **Dodaj usługę** znajduje się w tym menu powinna być klastra usługi HDInsight toohello usług używanych tooadd. Należy dodać nowe usługi za pomocą akcji skryptu podczas inicjowania obsługi klastra. Aby uzyskać więcej informacji dotyczących za pomocą akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

Podczas hello **akcje** przycisku można uruchomić ponownie wszystkie usługi, często ma toostart zatrzymanie i ponowne uruchamianie określonej usługi. Użyj hello, wykonując kroki tooperform akcje na pojedynczej usługi:

1. Z hello **pulpitu nawigacyjnego** lub **usług** wybierz opcję usługi.

2. Z góry hello hello **Podsumowanie** Użyj hello **akcji usługi** przycisk i wybierz hello tootake akcji. Spowoduje to ponowne uruchomienie usługi hello we wszystkich węzłach.

    ![działanie usługi](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Ponowne uruchamianie niektórych usług uruchomionej hello klastra może generować alerty. tooavoid alertów, można użyć hello **akcji usługi** tooenable przycisk **trybu konserwacji** hello usługi przed wykonaniem hello ponownego uruchomienia komputera.

3. Po wybraniu akcji hello **# op** wpis u góry hello hello strony zwiększa tooshow, która jest wykonywana operacji w tle. Jeśli skonfigurowano toodisplay, zostanie wyświetlona lista hello operacje w tle.

   > [!NOTE]
   > Jeśli włączono **trybu konserwacji** usługi hello Pamiętaj toodisable go za pomocą hello **akcji usługi** przycisku po zakończeniu operacji hello.

tooconfigure usługi, użyj hello następujące kroki:

1. Z hello **pulpitu nawigacyjnego** lub **usług** wybierz opcję usługi.

2. Wybierz hello **Configs** kartę hello bieżącej konfiguracji jest wyświetlany. Wyświetlana jest również lista poprzedniej konfiguracji.

    ![Konfiguracje](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Użyj hello pola wyświetlane toomodify hello konfiguracji, a następnie wybierz **zapisać**. Lub wybierz poprzednią konfigurację, a następnie wybierz **stać się bieżącym** tooroll kopii toohello poprzednie ustawienia.

## <a name="ambari-views"></a>Widoki Ambari

Widoki Ambari pozwalają deweloperom tooplug elementy interfejsu użytkownika do hello Ambari Web UI za pomocą hello [Framework widoków Ambari](https://cwiki.apache.org/confluence/display/AMBARI/Views). Usługa HDInsight zapewnia hello następujące widoki z typami klastra usługi Hadoop:

* Yarn menedżera kolejek: hello menedżera kolejek udostępnia prosty interfejs do wyświetlanie i modyfikowanie kolejek YARN.

* Widok hive: hello Hive View pozwala toorun zapytań programu Hive bezpośrednio z przeglądarki sieci web. Możesz zapisać zapytania, wyświetlić wyniki, zapisane wyniki w magazynie klastra toohello lub pobrać systemu lokalnego tooyour wyników. Aby uzyskać więcej informacji na korzystanie z widoków Hive, zobacz [Użyj widoki Hive z usługą HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

* Widok tez: hello widoku Tez pozwala toobetter zrozumieć i zoptymalizować zadania. Można wyświetlać informacje w sposób Tez zadania są wykonywane, i jakie zasoby są używane.
