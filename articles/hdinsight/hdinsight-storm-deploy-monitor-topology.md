---
title: "aaaDeploy i zarządzanie topologiami Apache Storm na HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy, monitorować i zarządzać nimi za pomocą hello pulpit nawigacyjny Storm w usłudze HDInsight topologii Apache Storm. Narzędzia usługi Hadoop dla programu Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Windows

pulpit nawigacyjny Storm Hello umożliwia tooeasily wdrażanie i uruchamianie klastra usługi HDInsight tooyour topologii Apache Storm za pomocą przeglądarki sieci web. Można również użyć hello toomonitor pulpitu nawigacyjnego i zarządzania uruchomionymi topologiami. Jeśli używasz programu Visual Studio hello narzędzia HDInsight Tools for Visual Studio zapewniają podobne funkcje w programie Visual Studio.

Hello pulpit nawigacyjny Storm i funkcje Storm hello hello narzędzi HDInsight Tools korzystają z interfejsu API REST Storm, które mogą być używane toocreate hello własnych rozwiązań do zarządzania i monitorowania.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają Storm w klastrze usługi HDInsight, z systemem Windows jako hello systemu operacyjnego. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Aby uzyskać informacje dotyczące wdrażania i zarządzania topologii Storm z klastrem usługi HDInsight, który używa systemu Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Wymagania wstępne

* **Apache Storm w usłudze HDInsight** — zobacz [wprowadzenie do Apache Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started.md) instrukcje dotyczące tworzenia klastra.

* Dla hello **pulpitu nawigacyjnego Storm**: przeglądarki nowoczesnych witryn sieci web, która obsługuje protokół HTML5.

* Dla **programu Visual Studio** -zestawu Azure SDK 2.5.1 lub nowszej i hello narzędzi HDInsight Tools for Visual Studio. Zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall i skonfigurować hello HDInsight tools for Visual Studio.

    Jedna z hello następujące wersje programu Visual Studio:

  * Program Visual Studio 2012 z aktualizacją 4

  * Visual Studio 2013 z aktualizacją 4 lub Visual Studio 2013 Community

  * Visual Studio 2015 (dowolna wersja)

  * Visual Studio 2017 (dowolna wersja)

## <a name="storm-dashboard"></a>Pulpit nawigacyjny STORM

Hello pulpit nawigacyjny Storm jest dostępne na klaster Storm strony sieci web. adres URL Hello jest **https://&lt;clustername >.azurehdinsight.net/**, gdzie **clustername** jest nazwą hello Storm w klastrze usługi HDInsight.

Z góry hello hello pulpit nawigacyjny Storm, wybierz **przesyłania topologii**. Postępuj zgodnie z instrukcjami hello na powitania strony toorun przykładowa topologia lub tooupload i uruchom topologii, który został utworzony.

![Witaj przesyłania topologii strony][storm-dashboard-submit]

### <a name="storm-ui"></a>STORM interfejsu użytkownika

Hello pulpit nawigacyjny Storm, zaznacz hello **interfejsu użytkownika platformy Storm** łącza. Informacje o klastrze hello, spowoduje to wyświetlenie w tooany dodanie uruchomionymi topologiami.

![Witaj interfejsu użytkownika platformy storm][storm-dashboard-ui]

> [!NOTE]
> W niektórych wersjach programu Internet Explorer może stwierdzić, że powitalne interfejsu użytkownika platformy Storm nie powoduje odświeżenia po raz pierwszy odwiedzeniu go. Na przykład może nie pokazywać topologii nowy hello przesłane lub mogą być wyświetlane topologii jako aktywny, gdy wcześniej dezaktywowana. Firma Microsoft zna tego problemu i pracuje nad rozwiązaniem.

#### <a name="main-page"></a>Strona główna

strony główne Hello hello interfejsu użytkownika platformy Storm udostępnia hello następujących informacji:

* **Podsumowanie klastra**: podstawowe informacje o hello klaster Storm.

* **Topologia podsumowania**: Lista uruchomionych topologii. Użyj hello łącza w tej sekcji tooview więcej informacji o określonych topologii.

* **Podsumowanie przełożonego**: informacje o przełożonego Storm hello.

* **Konfiguracja nimbus**: Konfiguracja Nimbus hello klastra.

#### <a name="topology-summary"></a>Topologia podsumowania

Wybieranie łącza z hello **podsumowanie topologii** sekcja wyświetla następujące informacje o topologii hello hello:

* **Topologia podsumowania**: podstawowe informacje o topologii hello.

* **Akcje topologii**: Akcje zarządzania, które można wykonywać w odniesieniu do topologii hello.

  * **Aktywuj**: wznowienie przetwarzania dezaktywowanej topologii.

  * **Dezaktywuj**: wstrzymanie uruchomionej topologii.

  * **Rebalance**: można dostosować równoległość hello hello topologii. Po zmianie hello liczby węzłów w klastrze hello, należy przeprowadzić ponowne równoważenie uruchomionych topologii. Dzięki temu hello topologii tooadjust równoległości toocompensate dla hello zwiększyć lub zmniejszyć liczbę węzłów w klastrze hello.

      Aby uzyskać więcej informacji, zobacz [opis hello równoległości topologii Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kasowanie**: kończy topologii Storm po hello określony limit czasu.

* **Statystyka topologii**: Statystyka topologii hello. Użyj łączy hello w hello **okna** kolumny tooset hello ramy czasowe hello pozostałe wpisy na stronie powitania.

* **Spouts**: hello elementach spout używane przez hello topologii. Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementach spout.

* **Bolts**: hello używane przez hello topologii elementów bolt. Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementów bolt.

* **Topologia konfiguracji**: hello konfiguracji topologii hello wybrane.

#### <a name="spout-and-bolt-summary"></a>Spout i Bolt — podsumowanie

Wybieranie spout z hello **Spouts** lub **Bolts** sekcje Wyświetla hello następujących informacji o elemencie hello wybrane:

* **Składnik podsumowania**: podstawowe informacje o hello spout lub bolt.

* **Spout/Bolt stats**: Statystyka hello spout lub elementów bolt. Użyj łączy hello w hello **okna** kolumny tooset hello ramy czasowe hello pozostałe wpisy na stronie powitania.

* **Wprowadź statystykę** (tylko dla elementów bolt): informacje o hello strumienie używane przez hello bolt.

* **OUTPUT stats**: informacje o strumieni hello emitowane przez to spout ani dla elementów bolt.

* **Modułów**: informacje na temat wystąpień hello hello spout lub bolt. Wybierz hello **portu** wpis dla tooview określonego modułu wykonującego dziennika informacji diagnostycznych utworzone dla tego wystąpienia.

* **Błędy**: informacje o błędzie dla tego spout lub elementów bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>HDInsight Tools for Visual Studio

Narzędzia HDInsight Hello mogą być używane toosubmit C# i hybrydowych topologii tooyour klaster Storm. Witaj, wykonaj czynności użyć przykładowej aplikacji. Informacji o tworzeniu własnych topologii za pomocą narzędzi HDInsight hello, zobacz [topologii opracowywania C# za pomocą hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Użyj następujących hello kroki toodeploy tooyour próbki Storm w klastrze usługi HDInsight, a następnie Wyświetl i Zarządzaj hello topologii.

1. Jeśli nie został już zainstalowany hello najnowszą wersję hello narzędzi HDInsight Tools for Visual Studio, zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Otwórz program Visual Studio, wybierz **pliku** > **nowy** > **projektu**.

3. W hello **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **szablony**, a następnie wybierz **HDInsight**. Wybierz z listy hello szablonów **próbki Storm**. U dołu hello hello — okno dialogowe wpisz nazwę aplikacji hello.

    ![Obraz](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.

   > [!NOTE]
   > Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania hello subskrypcji platformy Azure. Jeśli masz więcej niż jedną subskrypcję, zaloguj się za toohello, który zawiera Storm w klastrze usługi HDInsight.

5. Wybierz Storm w klastrze usługi HDInsight z hello **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**. Można monitorować, czy przesyłanie hello działa prawidłowo, używając hello **dane wyjściowe** okna.

6. Gdy topologia hello został pomyślnie przesłany, hello **topologii Storm** dla klastra hello powinna zostać wyświetlona. Wybierz topologię hello z hello listy tooview informacji na temat hello systemem topologii.

    ![monitor programu Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > Można również wyświetlić **topologii Storm** z **Eksploratora serwera** rozwijając **Azure** > **HDInsight**, a następnie prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierając **topologii Storm widoku**.

    Wybierz kształt hello hello spouts lub bolts tooview informacji dotyczących tych składników. Otwiera nowe okno dla każdego wybranego elementu.

   > [!NOTE]
   > Nazwa Hello topologii hello jest nazwą klasy hello topologii hello (w tym przypadku `HelloWord`,) z sygnaturą czasową dołączane.

7. Z hello **podsumowanie topologii** widok, wybierz opcję **Kill** toostop hello topologii.

   > [!NOTE]
   > Topologii STORM nadal działać do chwili zostały zatrzymane lub hello klastra zostanie usunięta.


## <a name="rest-api"></a>Interfejs API REST

Hello interfejsu użytkownika platformy Storm jest oparty na powitania interfejsu API REST, więc można wykonać podobne do zarządzania i monitorowania funkcji przy użyciu hello interfejsu API REST. Można użyć interfejsu API REST hello toocreate niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.

Aby uzyskać więcej informacji, zobacz [interfejsu API REST interfejsu użytkownika Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Witaj następujące informacje są hello toousing określonego interfejsu API REST z systemu Apache Storm w usłudze HDInsight.

### <a name="base-uri"></a>Podstawowy identyfikator URI

Hello jest podstawowy identyfikator URI dla hello interfejsu API REST w klastrach HDInsight **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, gdzie **clustername** jest nazwą hello Storm na Klaster usługi HDInsight.

### <a name="authentication"></a>Authentication

Toohello żądania interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, więc użyć hello HDInsight klastra nazwę i hasło administratora.

> [!NOTE]
> Ponieważ uwierzytelnianie podstawowe jest wysyłany przy użyciu zwykłego tekstu, należy **zawsze** połączeń toosecure HTTPS za pomocą hello klastra.

### <a name="return-values"></a>Wartości zwracane

Informacje zwrócone z hello interfejsu API REST mogą być tylko można używać z wewnątrz klastra hello lub maszyn wirtualnych na hello tej samej sieci wirtualnej platformy Azure jako klaster hello. Na przykład hello pełną nazwę domeny (FQDN) dla serwerów dozorcy zwracane są nie być dostępny z Internetu hello.

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już jak topologie toodeploy i monitorować za pomocą hello pulpit nawigacyjny Storm, Dowiedz się jak:

* [Opracowywanie topologii C# za pomocą hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Opracowywanie topologii opartych na języku Java za pomocą programu Maven](hdinsight-storm-develop-java-topology.md)

Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
