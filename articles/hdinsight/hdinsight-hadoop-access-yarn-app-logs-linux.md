---
title: "rejestruje aaaAccess Hadoop YARN aplikacji w usłudze HDInsight opartych na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dzienniki tooaccess YARN aplikacji w klastrze opartych na systemie Linux usługą HDInsight (Hadoop), używając hello wiersza polecenia i przeglądarki sieci web."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Dzienniki aplikacji YARN dostępu w usłudze HDInsight z systemem Linux

Dowiedz się, jak tooaccess hello dzienników YARN (jeszcze inny zasób moduł negocjowania) aplikacji na klastra usługi Hadoop w usłudze Azure HDInsight.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>YARN osi czasu serwera

Witaj [YARN osi czasu serwera](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) zawiera ogólne informacje dotyczące aplikacji ukończone i informacje o określonej struktury aplikacji za pomocą dwóch różnych interfejsów. W szczególności:

* Przechowywanie i pobieranie informacji o aplikacji ogólnego w klastrach HDInsight została włączona w wersji 3.1.1.374 lub nowszej.
* składnik informacji określonej struktury aplikacji Hello hello osi czasu serwera nie jest aktualnie dostępny w klastrach usługi HDInsight.

Ogólne informacje na temat aplikacji obejmuje hello następującego typu danych:

* Identyfikator aplikacji Hello, unikatowy identyfikator aplikacji
* Witaj użytkownika, który uruchomił aplikacji hello
* Informacje prób logowania dokonanych aplikacji hello toocomplete
* kontenery Hello używane przez wszystkie próby danej aplikacji

## <a name="YARNAppsAndLogs"></a>Dzienniki YARN aplikacji i

YARN obsługuje wiele modele programowania (MapReduce jest jednym z nich) dzięki rozdzieleniu zarządzanie zasobami z planowania/monitorowania aplikacji. YARN używa globalnym *ResourceManager* (RM) na węzła procesu roboczego *NodeManagers* (NMs) i dla każdej aplikacji *ApplicationMasters* (AMs). Witaj AM poszczególnych aplikacji negocjuje zasobów (Procesora, pamięci, dysku, sieci) do uruchamiania aplikacji z hello Menedżera zasobów. Witaj RM współpracuje z NMs toogrant tych zasobów, które są przyznawane jako *kontenery*. Witaj AM jest odpowiedzialny za śledzenia hello postęp hello tooit kontenery przypisane przez hello Menedżera zasobów. Aplikacja może wymagać wiele kontenerów w zależności od charakteru aplikacji hello hello.

Każda aplikacja może składać się z wielu *prób aplikacji*. Jeśli aplikacja nie powiedzie się, może zostać powtórzone, jako nowego próba. Każda próba uruchamia się w kontenerze. W tym sensie kontener zawiera kontekst hello podstawowa jednostka pracy wykonanej przez aplikację YARN. Wszystkie pracy, którą można wykonać tylko w kontekście hello kontenera odbywa się w węźle pojedynczego procesu roboczego hello na powitania, która została przydzielona kontenera. Zobacz [pojęcia YARN] [ YARN-concepts] dla dalszego odwołania.

Dzienniki (Dzienniki aplikacji i skojarzonych hello kontenera) są krytyczne w debugowaniu problematyczne aplikacje platformy Hadoop. YARN umożliwia nieuprzywilejowany framework do zbierania, agregację i przechowywania Dzienniki aplikacji z hello [agregacji dziennika] [ log-aggregation] funkcji. funkcja agregacji dziennika Hello umożliwia teraz bardziej przewidywalna podczas uzyskiwania dostępu do dzienników aplikacji. Go łączy dzienników wszystkich kontenerów w węźle procesu roboczego i przechowuje je jako jeden zagregowany plik dziennika na węzła procesu roboczego. Hello dziennika są przechowywane na powitania domyślnego systemu plików, po zakończeniu działania aplikacji. Aplikacja może korzystać z setkami lub tysiącami kontenerów, ale dzienniki dla wszystkich kontenerów uruchomiona w węźle pojedynczego procesu roboczego są zawsze zagregowane tooa pojedynczy plik. To jest tylko 1 dziennika w każdym węźle procesu roboczego używany przez aplikację. Agregacja dziennika jest domyślnie włączone w klastrach usługi HDInsight w wersji 3.0 lub nowszym. Zagregowane Dzienniki znajdują się w domyślny magazyn dla klastra hello. Witaj ze ścieżką jest dzienniki toohello ścieżki systemu plików HDFS hello:

    /app-logs/<user>/logs/<applicationId>

W ścieżce hello `user` jest nazwą hello hello użytkownika, który uruchomił aplikacji hello. Witaj `applicationId` jest hello Unikatowy identyfikator przypisany tooan aplikacja hello YARN Menedżera zasobów.

Witaj zagregowane dzienniki nie są bezpośrednio do odczytu, ponieważ są one zapisywane [TFile][T-file], [format binarny] [ binary-format] indeksowane według kontenera. Użyj hello dzienników YARN ResourceManager lub interfejsu wiersza polecenia narzędzia tooview te dzienniki jako zwykły tekst dla aplikacji lub kontenery zainteresowań.

## <a name="yarn-cli-tools"></a>Narzędzia YARN interfejsu wiersza polecenia

toouse hello YARN interfejsu wiersza polecenia narzędzia, należy najpierw połączyć toohello klastra usługi HDInsight przy użyciu protokołu SSH. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Te dzienniki można wyświetlić jako zwykły tekst, uruchamiając jeden z hello następującego polecenia:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Określ hello &lt;applicationId >, &lt;-który — uruchomiona — aplikacji użytkownika >, &lt;identyfikatora kontenera >, i &lt;adres przypisany węzła procesu roboczego > informacje po uruchomieniu tych poleceń.

## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager UI

Witaj w interfejsie użytkownika YARN ResourceManager działa na hello headnode klastra. Jest on dostępny za pośrednictwem sieci web Ambari hello interfejsu użytkownika. Następujące kroki tooview hello YARN hello Użyj dzienników:

1. W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net. Zamień NAZWAKLASTRA hello nazwę klastra usługi HDInsight.
2. Wybierz z listy hello usług po lewej stronie powitania **YARN**.

    ![Wybrana usługa yarn](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. Z hello **szybkie linki** listy rozwijanej wybierz jedną z głównymi węzłami klastra hello, a następnie wybierz **dziennika ResourceManager**.

    ![Yarn szybkie linki](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Jest wyświetlana lista dzienników tooYARN łącza.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
