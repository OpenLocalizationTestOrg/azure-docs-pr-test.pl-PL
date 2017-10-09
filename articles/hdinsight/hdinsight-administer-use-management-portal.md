---
title: "aaaManage opartych na systemie Windows klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadminister usługi HDInsight. Tworzenie klastra HDInsight, otwórz hello interakcyjne konsoli języka JavaScript i otwórz hello Hadoop polecenia konsoli."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Zarządzanie oparte na systemie Windows klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello portalu Azure

Przy użyciu hello [portalu Azure][azure-portal], można utworzyć klastry z systemem Windows Hadoop w usłudze Azure HDInsight, Zmień hasło użytkownika Hadoop i Włącz protokół RDP (Remote Desktop) umożliwi dostęp hello Hadoop konsoli poleceń w klastrze hello.

Witaj informacje w tym artykule ma zastosowanie tylko na podstawie tooWindow klastrów usługi HDInsight. Aby uzyskać informacje na temat zarządzania opartych na systemie Linux klastrów, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).


## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Konto usługi Azure Storage** -klastra usługi HDInsight używa kontenera magazynu obiektów Blob platformy Azure jako hello domyślnego systemu plików. Aby uzyskać więcej informacji o sposobie magazynu obiektów Blob Azure zapewnia bezproblemową obsługę z klastrami usługi HDInsight, zobacz [Użyj magazynu obiektów Blob Azure z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md). Aby uzyskać więcej informacji na temat tworzenia konta usługi Azure Storage, zobacz [jak tooCreate konta magazynu](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Otwórz Portal hello
1. Zaloguj się za[https://portal.azure.com](https://portal.azure.com).
2. Po otwarciu portalu hello można:

   * Kliknij przycisk **nowy** z toocreate menu po lewej stronie powitania nowego klastra:

       ![przycisk Nowy klaster usługi HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Kliknij przycisk **klastrów usługi HDInsight** z menu po lewej stronie powitania.

       ![Przycisk klastra usługi HDInsight portalu Azure](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Jeśli **HDInsight** nie są wyświetlane w menu po lewej stronie powitania kliknij pozycję **Przeglądaj**.

     ![Przycisk klastra przeglądania portalu Azure](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Tworzenie klastrów
Instrukcje tworzenia hello przy użyciu hello portalu można znaleźć [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

HDInsight działa ze składnikami szeroki zakres Hadoop. Lista hello hello składników, które zostały zweryfikowane i obsługiwane, [jest wersję platformy Hadoop w usłudze Azure HDInsight](hdinsight-component-versioning.md). HDInsight można dostosować za pomocą jednego z hello następujące opcje:

* Użyj akcji skryptu toorun niestandardowe skrypty, które można dostosować tooeither klastra zmianę konfiguracji klastra lub zainstalować składniki niestandardowe, takie jak Giraph lub Solr. Aby uzyskać więcej informacji, zobacz [dostosować klastra usługi HDInsight przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster.md).
* Parametry hello klastra dostosowania hello zestawu .NET SDK usługi HDInsight lub programu PowerShell systemu Azure podczas tworzenia klastra. Te zmiany w konfiguracji są następnie zachowywane przez okres istnienia hello hello klastra i nie dotyczy reimages węzła klastra, które platformy Azure okresowo przesyła konserwacji. Aby uzyskać więcej informacji na temat używania parametrów dostosowania klastra hello, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Niektóre składniki natywnego języka Java, takich jak Mahout i usuwania kaskadowego, można uruchomić w klastrze hello jako pliki JAR. Te pliki JAR mogą być rozproszone tooAzure magazynu obiektów Blob i przesłać tooHDInsight klastrów za pomocą mechanizmów przesyłanie zadań Hadoop. Aby uzyskać więcej informacji, zobacz [Hadoop przesyłania zadania programowo](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Jeśli masz problemy z wdrażanie klastrów tooHDInsight pliki JAR lub wywoływania pliki JAR w klastrach HDInsight, skontaktuj się z [Microsoft Support](https://azure.microsoft.com/support/options/).
  >
  > Kaskadowe nie jest obsługiwany przez usługi HDInsight, a nie jest uprawniony do firmy Microsoft Support. Aby uzyskać listę obsługiwanych składników, zobacz [nowości w wersjach klastra hello dostarczanych z usługą HDInsight](hdinsight-component-versioning.md).
  >
  >

Instalacja oprogramowania niestandardowe na powitania klastra przy użyciu usługi Podłączanie pulpitu zdalnego nie jest obsługiwana. Należy unikać przechowywania plików na dyskach hello hello węzła głównego, jak będą utracone, jeśli potrzebujesz toore — Tworzenie klastrów hello. Zalecane jest przechowywanie plików w magazynie obiektów Blob platformy Azure. Magazyn obiektów blob jest trwały.

## <a name="list-and-show-clusters"></a>Lista i Pokaż klastrów
1. Zaloguj się za[https://portal.azure.com](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** z menu po lewej stronie powitania.
3. Kliknij nazwę klastra hello. Jeśli lista klastrów hello jest długa, można użyć filtru u góry hello hello strony.
4. Kliknij dwukrotnie klastra z hello listy tooshow hello szczegóły.

    **Menu i essentials**:

    ![Essentials klastra usługi HDInsight portalu Azure](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * toocustomize hello menu, kliknij prawym przyciskiem myszy na powitania menu, a następnie kliknij **Dostosuj**.
   * **Ustawienia** i **wszystkie ustawienia**: Wyświetla hello **ustawienia** bloku hello klastra, dzięki czemu można tooaccess szczegółowe informacje o konfiguracji dla hello klastra.
   * **Pulpit nawigacyjny**, **pulpit nawigacyjny klastra** i **adresu URL: są to wszystkie sposoby tooaccess hello klastra pulpitu nawigacyjnego, który jest sieci Ambari Web w klastrach opartych na systemie Linux. -**Bezpiecznej powłoki **: Pokazuje hello instrukcje tooconnect toohello klastra przy użyciu połączenia protokołu Secure Shell (SSH).
   * **Skalowanie klastra**: umożliwia toochange hello liczba węzłów procesu roboczego dla tego klastra.
   * **Usuń**: usuwa hello klastra.
   * **Szybki Start**: Wyświetla informacje, które pomogą Ci rozpocząć korzystanie z usługi HDInsight.
   * ** Użytkownicy: Umożliwia uprawnienia tooset *portalu zarządzania* klastra dla innych użytkowników w Twojej subskrypcji platformy Azure.

     > [!IMPORTANT]
     > To *tylko* dotyczy klastra toothis dostępu i innych uprawnień w hello portalu Azure i nie ma wpływu na łączących z klastrem usługi HDInsight toohello tooor przesyłania zadania.
     >
     >
   * **Tagi**: tagi Zezwalaj możesz tooset klucza i wartości pary toodefine niestandardowych taksonomii usług w chmurze. Na przykład może utworzyć klucz o nazwie **projektu**, a następnie użyć wspólną wartość wszystkie usługi powiązane z określonego projektu.
   * **Widoki Ambari**: łączy tooAmbari sieci Web.

     > [!IMPORTANT]
     > toomanage hello usługi świadczone przez hello klastra usługi HDInsight, należy użyć narzędzia Ambari Web lub hello interfejsu API REST Ambari. Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Użycie**:

     ![Obciążenie klastra usługi HDInsight portalu Azure](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Kliknij przycisk **ustawienia**.

    ![Obciążenie klastra usługi HDInsight portalu Azure](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Właściwości**: Wyświetl hello właściwości klastra.
   * **Tożsamość usługi AAD klastra**:
   * **Klucze magazynu Azure**: Wyświetl hello domyślne konto magazynu i klucza. Konto magazynu Hello jest konfiguracji podczas procesu tworzenia klastra hello.
   * **Klaster logowania**: Zmień nazwę użytkownika klastra HTTP hello i hasło.
   * **Zewnętrzne magazyny**: Wyświetl hello Hive i Oozie magazyny. Magazyny Hello można skonfigurować tylko podczas procesu tworzenia klastra hello.
   * **Skalowanie klastra**: Zwiększ i zmniejszenie hello liczba węzłów procesu roboczego w klastrze.
   * **Pulpit zdalny**: Włącz i Wyłącz dostęp do usług pulpitu zdalnego (RDP) i skonfiguruj hello RDP username.  Nazwa użytkownika pulpitu zdalnego Hello musi być inna niż nazwa użytkownika hello HTTP.
   * **Partnera partner of Record**:

     > [!NOTE]
     > Jest to rodzajowy lista dostępnych ustawień; nie wszystkie z nich będzie stosowany w przypadku wszystkich typów klastra.
     >
     >
6. Kliknij przycisk **właściwości**:

    Sekcja właściwości Hello wymieniono poniżej hello:

   * **Nazwa hosta**: Nazwa klastra.
   * **Adres URL klastra**.
   * **Stan**: obejmują zostało przerwane, zaakceptowane, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, operacyjne, uruchomione, błąd, usuwanie, usunięty, upłynął limit czasu, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, ClusterCustomization CertRolloverQueued, ResizeQueued,
   * **Region**: Lokalizacja platformy Azure. Aby uzyskać listę obsługiwanych lokalizacji platformy Azure, zobacz hello **Region** lista rozwijana na [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Dane utworzone**.
   * **System operacyjny**: albo **Windows** lub **Linux**.
   * **Typ**: Hadoop, HBase, Storm, Spark.
   * **Wersja**. Zobacz [wersji usługi HDInsight](hdinsight-component-versioning.md)
   * **Subskrypcja**: Nazwa subskrypcji.
   * **Identyfikator subskrypcji**.
   * **Podstawowe źródło danych**. Witaj konta magazynu obiektów Blob platformy Azure używana jako domyślna hello systemu plików usługi Hadoop.
   * **Warstwa cenowa węzłów procesu roboczego**.
   * **Warstwę cenową węzła HEAD**.

## <a name="delete-clusters"></a>Usuwanie klastrów
Usunięcie klastra nie spowoduje usunięcia hello domyślne konto magazynu lub wszystkie połączone konta magazynu. Można ponownie utworzyć klaster hello przy użyciu hello tego samego konta magazynu i hello tego samego magazyny.

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **Przeglądaj wszystko** w menu po lewej stronie powitania kliknij **klastrów usługi HDInsight**, kliknij swoją nazwę klastra.
3. Kliknij przycisk **usunąć** z hello menu u góry, a następnie wykonaj instrukcje hello.

Zobacz też [Wstrzymaj/zamykania klastrów](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Skalowanie klastrów
Skalowanie funkcji klastra Hello umożliwia toochange hello liczba węzłów procesu roboczego, używane przez klaster działa w usłudze Azure HDInsight bez konieczności toore — Tworzenie klastra hello.

> [!NOTE]
> Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane. Jeśli masz pewności, jaka wersja hello klastra, można sprawdzić hello stronę właściwości.  Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).
>
>

wpływ Hello Zmienianie hello liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:

* Usługa Hadoop

    Można zwiększyć bezproblemowo hello liczba węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania. W trakcie operacji hello również można przesłać nowe zadania. Błędy w operacji skalowania bezpiecznie obsługi tak, aby hello klastra zawsze pozostanie w stanie funkcjonalności.

    Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby hello węzły danych są ponownie uruchamiane niektórych usług hello hello klastra. Powoduje to wszystkich uruchomionych i oczekujących zadań toofail na zakończenie hello hello operacji skalowania. Można jednak Prześlij ponownie hello zadania po zakończeniu operacji hello.
* HBase

    Można bezproblemowo dodać lub usunąć klaster HBase tooyour węzłów, jest uruchomiona. Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia hello operacji skalowania. Można jednak również ręcznie saldo serwerów regionalnych hello logując się do headnode hello klastra i uruchomione hello poniższych poleceń z poziomu okna wiersza polecenia:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Aby uzyskać więcej informacji na temat używania powłoki HBase hello Zobacz]
* Storm

    Można bezproblemowo dodać lub usunąć klaster Storm tooyour węzłów danych jest uruchomiona. Jednak po pomyślnym zakończeniu hello operacji skalowania, konieczne będzie toorebalance hello topologii.

    Ponowne równoważenie można zrobić na dwa sposoby:

  * STORM interfejsu użytkownika sieci web
  * Narzędzia interfejsu wiersza polecenia (CLI)

    Zobacz toohello [dokumentację Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) więcej szczegółów.

    Witaj interfejsu użytkownika sieci web platformy Storm w klastrze jest dostępny hello HDInsight:

    ![Zrównoważ skali storm w usłudze HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Poniżej przedstawiono przykładowy sposób hello toouse interfejsu wiersza polecenia polecenie topologii Storm hello toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**klastry tooscale**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **Przeglądaj wszystko** w menu po lewej stronie powitania kliknij **klastrów usługi HDInsight**, kliknij swoją nazwę klastra.
3. Kliknij przycisk **ustawienia** z hello menu u góry, a następnie kliknij przycisk **klaster w skali**.
4. Wprowadź **węzłami liczba procesów roboczych**. limit Hello hello liczby węzłów klastra jest zależny od używanej subskrypcji platformy Azure. Możesz skontaktować się rozliczeń limit hello tooincrease pomocy technicznej.  informacje o kosztach Hello zostaną one zastosowane hello zmiany toohello liczba węzłów.

    ![Skala Spark Storm bazy danych HBase w usłudze HDInsight Hadoop](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Wstrzymaj/zamykania klastrów
Większość zadań usługi Hadoop to zadania wsadowe, które są tylko od czasu do czasu uruchomienia. Większość klastrów platformy Hadoop, istnieje duże okresów czasu hello klastra nie jest używany do przetwarzania. Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany.
Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany. Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane.

Istnieje wiele sposobów można program hello proces:

* Użytkownik fabryki danych Azure. Zobacz [połączoną usługą usługi HDInsight Azure](../data-factory/data-factory-compute-linked-services.md) i [transformacji i analizy przy użyciu fabryki danych Azure](../data-factory/data-factory-data-transformation-activities.md) dla usługi HDInsight na żądanie i samodzielnie zdefiniowanym połączone usługi.
* Za pomocą programu Azure PowerShell.  Zobacz [analizowanie danych opóźnienie transmitowane](hdinsight-analyze-flight-delay-data.md).
* Za pomocą interfejsu wiersza polecenia platformy Azure. Zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu wiersza polecenia Azure](hdinsight-administer-use-command-line.md).
* Używanie zestawu SDK .NET usługi HDInsight. Zobacz [Hadoop przesyłania zadań](hdinsight-submit-hadoop-jobs-programmatically.md).

Aby hello uzyskać informacje o cenach, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete klastra z hello portalu, zobacz [usuwać klastry](#delete-clusters)

## <a name="change-cluster-username"></a>Zmiana nazwy użytkownika z klastra
Klaster usługi HDInsight mogą być dwa konta użytkownika. podczas procesu tworzenia hello jest tworzony Hello konta użytkownika klastra usługi HDInsight. Można również utworzyć konto użytkownika RDP do uzyskiwania dostępu do klastra hello za pomocą protokołu RDP. Zobacz [Włącz pulpit zdalny](#connect-to-hdinsight-clusters-by-using-rdp).

**Nazwa użytkownika klastra usługi HDInsight hello toochange i hasło**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **Przeglądaj wszystko** w menu po lewej stronie powitania kliknij **klastrów usługi HDInsight**, kliknij swoją nazwę klastra.
3. Kliknij przycisk **ustawienia** z hello menu u góry, a następnie kliknij przycisk **logowania do klastra**.
4. Jeśli **logowania do klastra** została włączona, należy kliknąć opcję **wyłączyć**, a następnie kliknij przycisk **włączyć** przed zmianą hello nazwy użytkownika i hasła..
5. Zmiany hello **nazwa logowania klastra** i/lub hello **hasło logowania klastra**, a następnie kliknij przycisk **zapisać**.

    ![HDInsight zmienić http klastra użytkownika nazwy użytkownika hasło](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Dostęp do przydzielenia/odwołania
Klastry HDInsight są powitania po HTTP usługi sieci web (wszystkie te usługi mają RESTful punkty końcowe):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Domyślnie te usługi są przyznawane dostępu. Możesz można odwołać/Udziel dostępu hello z hello portalu Azure.

> [!NOTE]
> Przez przyznawanie/odwoływanie dostępu hello, spowoduje zresetowanie hello klastra nazwę i hasło użytkownika.
>
>

**dostęp do usług sieci web toogrant/revoke HTTP**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **Przeglądaj wszystko** w menu po lewej stronie powitania kliknij **klastrów usługi HDInsight**, kliknij swoją nazwę klastra.
3. Kliknij przycisk **ustawienia** z hello menu u góry, a następnie kliknij przycisk **logowania do klastra**.
4. Jeśli **logowania do klastra** została włączona, należy kliknąć opcję **wyłączyć**, a następnie kliknij przycisk **włączyć** przed zmianą hello nazwy użytkownika i hasła..
5. Dla **nazwa użytkownika logowania klastra** i **hasło logowania klastra**, wprowadź hello nową nazwę użytkownika i hasło (odpowiednio) hello klastra.
6. Kliknij przycisk **SAVE** (Zapisz).

    ![HDInsight sumy Usuń dostęp do usługi sieci web http](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Znajdź hello domyślne konto magazynu
Każdy klaster usługi HDInsight ma domyślne konto magazynu. Witaj domyślne konto magazynu i kluczy dla klastra jest wyświetlana w obszarze **ustawienia**/**właściwości**/**klucze magazynu Azure**. Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Znajdź hello grupy zasobów
W trybie Azure Resource Manager hello każdego klastra usługi HDInsight jest tworzony z grupy zasobów platformy Azure. Grupa zasobów platformy Azure Hello klastra należy tooappears w:

* Lista klastrów Hello ma **grupy zasobów** kolumny.
* Klaster **podstawowych** kafelka.  

Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Otwórz konsolę usługi HDInsight zapytania
Hello konsoli zapytania HDInsight obejmuje hello następujące funkcje:

* **Edytor hive**: interfejs sieci web graficznego interfejsu użytkownika A przesyłania zadań Hive.  Zobacz [uruchamianie zapytań Hive przy użyciu hello konsoli zapytania](hdinsight-hadoop-use-hive-query-console.md).

    ![Edytor portalu hive HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Historia zadania**: Monitor Hadoop zadania.  

    ![HDInsight historii zadań portalu](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Kliknij przycisk **nazwa zapytania** właściwości zadania, w tym szczegóły hello tooshow **zapytanie dotyczące zadań**, i ** dane wyjściowe zadania. Możesz również pobrać zarówno hello zapytania, jak i stacji roboczej tooyour dane wyjściowe hello.
* **Przeglądarka plików**: przeglądanie hello domyślne konto magazynu i hello połączone konta magazynu.

    ![HDInsight portalu pliku przeglądarki przeglądania](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Na zrzucie ekranu pokazano hello hello  **<Account>**  typ wskazuje element hello jest konto magazynu platformy Azure.  Kliknij przycisk hello konta Nazwa toobrowse hello pliki.
* **Interfejs użytkownika Hadoop**.

    ![Portal usługi HDInsight Hadoop interfejsu użytkownika](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    Z **interfejsu użytkownika Hadoop*, przeglądać pliki, a w dzienniku.
* **Yarn interfejsu użytkownika**.

    ![Portal usługi HDInsight YARN interfejsu użytkownika](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Uruchamianie zapytań Hive
tooran zadań Hive z hello portalu, kliknij przycisk **Edytor Hive** w hello zapytania HDInsight konsoli. Zobacz [konsoli Otwórz zapytanie HDInsight](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Monitorowanie zadań
zadania toomonitor od hello portalu, kliknij przycisk **historii zadań** w hello zapytania HDInsight konsoli. Zobacz [konsoli Otwórz zapytanie HDInsight](#open-hdinsight-query-console).

## <a name="browse-files"></a>Przeglądanie plików
toobrowse pliki przechowywane w hello domyślne konto magazynu i hello połączone konta magazynu, kliknij przycisk **przeglądarka plików** w hello zapytania HDInsight konsoli. Zobacz [konsoli Otwórz zapytanie HDInsight](#open-hdinsight-query-console).

Można również użyć hello **Przeglądaj system plików hello** narzędzie z hello **interfejsu użytkownika Hadoop** w konsoli usługi HDInsight hello.  Zobacz [konsoli Otwórz zapytanie HDInsight](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Monitorowanie użycia klastra
Witaj **użycia** części bloku klastra usługi HDInsight hello Wyświetla informacje o hello liczba rdzeni tooyour dostępnych subskrypcji do użycia z usługą HDInsight, a także hello liczba rdzeni przydzielone toothis klastra i sposób ich przydzielone dla węzłów hello w tym klastrze. Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello usługi świadczone przez hello klastra usługi HDInsight, należy użyć narzędzia Ambari Web lub hello interfejsu API REST Ambari. Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Otwórz Hadoop interfejsu użytkownika
toomonitor hello klastra, system plików hello przeglądania i sprawdź dzienniki, kliknij przycisk **interfejsu użytkownika Hadoop** w hello zapytania HDInsight konsoli. Zobacz [konsoli Otwórz zapytanie HDInsight](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Otwórz Yarn interfejsu użytkownika
toouse interfejs użytkownika Yarn, kliknij przycisk **interfejsie użytkownika Yarn** w hello zapytania HDInsight konsoli. Zobacz [konsoli Otwórz zapytanie HDInsight](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Połącz tooclusters za pomocą protokołu RDP
poświadczenia Hello klastra hello, podane podczas jego tworzenia Udostępnij toohello usług na powitania klastra, ale nie toohello samego klastra za pośrednictwem pulpitu zdalnego. Dostęp do usług pulpitu zdalnego można włączyć podczas udostępniania klastra lub po zainicjowaniu obsługi klastra. Instrukcje hello o włączenie pulpitu zdalnego podczas tworzenia sekcji [HDInsight tworzenia klastra](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable pulpitu zdalnego**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **Przeglądaj wszystko** w menu po lewej stronie powitania kliknij **klastrów usługi HDInsight**, kliknij swoją nazwę klastra.
3. Kliknij przycisk **ustawienia** z hello menu u góry, a następnie kliknij przycisk **pulpitu zdalnego**.
4. Wprowadź **wygasa**, **nazwa użytkownika pulpitu zdalnego** i **hasła pulpitu zdalnego**, a następnie kliknij przycisk **włączyć**.

    ![HDInsight Włączanie wyłączanie Konfigurowanie pulpitu zdalnego](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    Witaj wartości domyślne dla wygasa jest tydzień.

   > [!NOTE]
   > Umożliwia także hello zestawu .NET SDK HDInsight tooenable pulpitu zdalnego w klastrze. Użyj hello **EnableRdp** metody dla obiektu klienta HDInsight hello w następujących sposób hello: **klienta. EnableRdp (nazwa_klastra, lokalizacji, "rdpuser", "rdppassword" DateTime.Now.AddDays(6))**. Podobnie, toodisable pulpitu zdalnego w klastrze hello, można użyć **klienta. DisableRdp (clustername, lokalizacja)**. Aby uzyskać więcej informacji na temat tych metod, zobacz [odwołania do zestawu SDK .NET usługi HDInsight](http://go.microsoft.com/fwlink/?LinkId=529017). Ma to zastosowanie tylko w przypadku klastrów usługi HDInsight w systemie Windows.
   >
   >

**tooconnect tooa klastra za pomocą protokołu RDP**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **Przeglądaj wszystko** w menu po lewej stronie powitania kliknij **klastrów usługi HDInsight**, kliknij swoją nazwę klastra.
3. Kliknij przycisk **ustawienia** z hello menu u góry, a następnie kliknij przycisk **pulpitu zdalnego**.
4. Kliknij przycisk **Connect** i postępuj zgodnie z instrukcjami hello. Jeśli połączenie jest wyłączona, należy włączyć ją najpierw. Upewnij się, że przy użyciu nazwy użytkownika pulpitu zdalnego hello i hasła.  Nie można użyć poświadczeń użytkownika hello klastra.

## <a name="open-hadoop-command-line"></a>Otwórz wiersz polecenia usługi Hadoop
tooconnect toohello klastra przy użyciu pulpitu zdalnego i wiersza polecenia platformy Hadoop hello używany, musi najpierw włączono klaster toohello dostęp do usług pulpitu zdalnego zgodnie z opisem w poprzedniej sekcji hello.

**tooopen wiersza polecenia usługi Hadoop**

1. Połącz toohello klastra przy użyciu pulpitu zdalnego.
2. Witaj pulpitu, kliknij dwukrotnie **wiersza polecenia usługi Hadoop**.

    ![HDI. HadoopCommandLine][image-hadoopcommandline]

    Aby uzyskać więcej informacji o poleceniach Hadoop, zobacz [Hadoop polecenia odwołanie](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

W hello poprzedni zrzut ekranu nazwy folderu hello ma numer wersji usługi Hadoop hello osadzonych. numer wersji Hello można zmienione na podstawie hello wersja składników Hadoop hello zainstalowany w klastrze hello. Można użyć Hadoop środowiska zmienne toorefer toothose folderów. Na przykład:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Następne kroki
W tym artykule uzyskanych jak toocreate klastra usługi HDInsight przy użyciu hello portalu i jak tooopen hello narzędzia wiersza polecenia usługi Hadoop. toolearn więcej, zobacz następujące artykuły hello:

* [Administrowanie HDInsight przy użyciu programu Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia platformy Azure](hdinsight-administer-use-command-line.md)
* [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Przesyłanie zadań Hadoop programowo](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Rozpoczynanie pracy z usługą Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Jest wersję platformy Hadoop w usłudze Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Wiersz polecenia usługi Hadoop"
