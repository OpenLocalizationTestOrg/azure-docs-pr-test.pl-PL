---
title: "aaaAccess Hadoop YARN aplikacji programowo — rejestruje Azure | Dokumentacja firmy Microsoft"
description: "Dostęp do aplikacji programowo loguje klastra usługi Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Dzienniki aplikacji YARN dostępu w usłudze HDInsight z systemu Windows
W tym temacie wyjaśniono, jak tooaccess hello dzienników YARN (jeszcze inny zasób moduł negocjowania) aplikacji, które zakończyły się w klastrze z systemem Windows Hadoop w usłudze Azure HDInsight

> [!IMPORTANT]
> Witaj informacje w tym dokumencie dotyczą tylko na podstawie tooWindows klastrów usługi HDInsight. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Aby uzyskać informacje na temat uruchamiania YARN loguje się klastrów usługi HDInsight opartych na systemie Linux, zobacz [logowania YARN dostęp do aplikacji opartych na systemie Linux platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Wymagania wstępne
* Klaster usługi HDInsight opartej na systemie Windows.  Zobacz [klastrów systemu Windows, Utwórz Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>YARN osi czasu serwera
Witaj <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN osi czasu serwera</a> zawiera ogólne informacje na temat aplikacji ukończone również jako framework informacje specyficzne dla aplikacji za pomocą dwóch różnych interfejsów. W szczególności:

* Przechowywanie i pobieranie informacji o aplikacji ogólnego w klastrach HDInsight została włączona w wersji 3.1.1.374 lub nowszej.
* składnik informacji określonej struktury aplikacji Hello hello osi czasu serwera nie jest aktualnie dostępny w klastrach usługi HDInsight.

Ogólne informacje na temat aplikacji obejmuje hello następujące rodzaje danych:

* Identyfikator aplikacji Hello, unikatowy identyfikator aplikacji
* Witaj użytkownika, który uruchomił aplikacji hello
* Informacje prób logowania dokonanych aplikacji hello toocomplete
* kontenery Hello używane przez wszystkie próby danej aplikacji

W klastrach HDInsight te informacje będą przechowywane przez usługi Azure Resource Manager tooa historii magazynu w hello domyślnego kontenera domyślnego konta magazynu Azure. Za pomocą interfejsu API REST można pobrać tego ogólnego danych w aplikacjach zakończone:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Dzienniki YARN aplikacji i
YARN obsługuje wiele modele programowania (MapReduce jest jednym z nich) dzięki rozdzieleniu zarządzanie zasobami z planowania/monitorowania aplikacji. Odbywa się za pośrednictwem globalnym *ResourceManager* (RM) na węzła procesu roboczego *NodeManagers* (NMs) i dla każdej aplikacji *ApplicationMasters* (AMs). Witaj AM poszczególnych aplikacji negocjuje zasobów (Procesora, pamięci, dysku, sieci) do uruchamiania aplikacji z hello Menedżera zasobów. Witaj RM współpracuje z NMs toogrant tych zasobów, które są przyznawane jako *kontenery*. Witaj AM jest odpowiedzialny za śledzenia hello postęp hello tooit kontenery przypisane przez hello Menedżera zasobów. Aplikacja może wymagać wiele kontenerów w zależności od charakteru aplikacji hello hello.

Ponadto każda aplikacja może składać się z wielu *prób aplikacji* w kolejności toofinish w obecności hello awarii lub utraty toohello komunikacji między AM i Menedżera zasobów. W związku z tym kontenery są przyznawane tooa próba określonych aplikacji. W tym sensie kontener zawiera kontekst hello podstawowa jednostka pracy wykonanej przez aplikację YARN, a wszystkie pracy, którą można wykonać tylko w kontekście hello kontenera odbywa się w węźle pojedynczego procesu roboczego hello na powitania, która została przydzielona kontenera. Zobacz [pojęcia YARN] [ YARN-concepts] dla dalszego odwołania.

Dzienniki (Dzienniki aplikacji i skojarzonych hello kontenera) są krytyczne w debugowaniu problematyczne aplikacje platformy Hadoop. YARN umożliwia nieuprzywilejowany framework do zbierania, agregację i przechowywania Dzienniki aplikacji z hello [agregacji dziennika] [ log-aggregation] funkcji. funkcja agregacji dziennika Hello sprawia, że podczas uzyskiwania dostępu do dzienników aplikacji teraz bardziej przewidywalna, agreguje dzienniki we wszystkich kontenerów w węźle procesu roboczego i przechowuje je jako jeden zagregowany plik dziennika na węzła procesu roboczego na powitania domyślnego systemu plików, po zakończeniu działania aplikacji. Aplikacja może korzystać z setkami lub tysiącami kontenerów, ale dzienniki dla wszystkich kontenerów uruchomiona w węźle pojedynczego procesu roboczego zawsze będzie zagregowane tooa pojedynczy plik, co w jeden plik dziennika na węzła procesu roboczego używany przez aplikację. Agregacji dziennik jest domyślnie włączone w klastrach HDInsight (w wersji 3.0 lub nowszej), i dzienniki zagregowane znajduje się w kontenerze domyślna hello klastra w następującej lokalizacji hello:

    wasb:///app-logs/<user>/logs/<applicationId>

W tym miejscu *użytkownika* jest nazwą hello hello użytkownika, który uruchomił aplikacji hello i *applicationId* jest hello Unikatowy identyfikator aplikacji przypisany przez hello YARN Menedżera zasobów.

Witaj zagregowane dzienniki nie są bezpośrednio do odczytu, ponieważ są one zapisywane [TFile][T-file], [format binarny] [ binary-format] indeksowane według kontenera. YARN umożliwia interfejsu wiersza polecenia narzędzia toodump te dzienniki jako zwykły tekst dla aplikacji lub kontenery zainteresowań. Dzienniki te można wyświetlić jako zwykły tekst, uruchamiając jeden z hello następujące polecenia YARN bezpośrednio w węzłach klastra hello (po połączeniu tooit za pośrednictwem protokołu RDP):

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager UI
Witaj interfejsie użytkownika YARN ResourceManager działa na powitania headnode klastra i jest możliwy za pośrednictwem hello pulpitu nawigacyjnego portalu Azure:

1. Zaloguj się za[portalu Azure](https://portal.azure.com/).
2. W menu po lewej stronie powitania kliknij **Przeglądaj**, kliknij przycisk **klastrów usługi HDInsight**, kliknij przycisk klastra z systemem Windows mają tooaccess hello dzienniki YARN aplikacji.
3. W menu u góry hello, kliknij polecenie **pulpitu nawigacyjnego**. Zostanie wyświetlona strona otwarty w nowym oknie przeglądarki kartę o nazwie **HDInsight zapytania konsoli**.
4. Z **konsoli zapytania HDInsight**, kliknij przycisk **interfejsie użytkownika Yarn**.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
