---
title: "klastry aaaManage Hadoop w usłudze HDInsight przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i zarządzania klastrami HDInsight przy użyciu hello portalu Azure."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Zarządzanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello portalu Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Przy użyciu hello [portalu Azure][azure-portal], można zarządzać klastrów platformy Hadoop w usłudze Azure HDInsight. Selektor hello karty informacji na temat zarządzania klastrów platformy Hadoop w usłudze HDInsight przy użyciu innych narzędzi.

**Wymagania wstępne**

Przed rozpoczęciem tego artykułu, musi mieć hello następujące elementy:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Otwórz hello portalu
1. Zaloguj się za[https://portal.azure.com](https://portal.azure.com).
2. Po otwarciu portalu hello można:

   * Kliknij przycisk **nowy** z toocreate menu po lewej stronie powitania nowego klastra:

       ![przycisk Nowy klaster usługi HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Kliknij przycisk **klastrów usługi HDInsight** z hello toolist menu po lewej stronie hello istniejących klastrów

       ![Przycisk klastra usługi HDInsight portalu Azure](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Jeśli nie widzisz klastra usługi HDInsight, kliknij przycisk **więcej usług** w dolnej części listy hello Witaj, a następnie kliknij **klastrów usługi HDInsight** w obszarze hello **analizy i analiza** sekcja.


## <a name="create-clusters"></a>Tworzenie klastrów
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight działa ze składnikami szeroki zakres Hadoop. Lista hello hello składników, które zostały zweryfikowane i obsługiwane, [jest wersję platformy Hadoop w usłudze Azure HDInsight](hdinsight-component-versioning.md). Dla informacji o tworzeniu klastra ogólne hello, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Wymagania dotyczące kontroli dostępu

Należy określić subskrypcji platformy Azure, podczas tworzenia klastra usługi HDInsight. Tego klastra mogą być tworzone w nowej grupy zasobów platformy Azure lub istniejącej grupy zasobów. Program hello następujące kroki tooverify swoje uprawnienia do tworzenia klastrów usługi HDInsight:

- toouse istniejącą grupę zasobów.

    1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
    2. Kliknij przycisk **grup zasobów** z grup zasobów hello toolist menu po lewej stronie powitania.
    3. Kliknij grupę zasobów hello potrzebują toouse do tworzenia klastra usługi HDInsight.
    4. Kliknij przycisk **(IAM) kontroli dostępu**i sprawdź, czy użytkownik (lub grupy, który należy do) ma co najmniej hello grupy zasobów toohello dostępu współautora.

- toocreate nową grupę zasobów

    1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
    2. Kliknij przycisk **subskrypcji** z menu po lewej stronie powitania. Ma ona żółta ikona klucza. Zostanie wyświetlona lista subskrypcji.
    3. Kliknij subskrypcję hello użycie toocreate klastrów. 
    4. Kliknij przycisk **Moje uprawnienia**.  Widoczny jest Twoje [roli](../active-directory/role-based-access-control-what-is.md#built-in-roles) na powitania subskrypcji. Należy co najmniej klastra usługi HDInsight toocreate dostępu współautora.

Jeśli wystąpi błąd NoRegisteredProviderFound hello lub MissingSubscriptionRegistration hello, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Lista i Pokaż klastrów
1. Zaloguj się za[https://portal.azure.com](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** z hello toolist menu po lewej stronie hello istniejących klastrów.
3. Kliknij nazwę klastra hello. Jeśli lista klastrów hello jest długa, można użyć filtru u góry hello hello strony.
4. Kliknij klastra z strony Przegląd hello toosee listy hello:

    ![Essentials klastra usługi HDInsight portalu Azure](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Pulpit nawigacyjny**: Otwiera hello pulpitu nawigacyjnego klastrze, czyli sieci Ambari Web w klastrach opartych na systemie Linux.
    * **Secure Shell**: Pokazuje hello instrukcje tooconnect toohello klastra przy użyciu połączenia protokołu Secure Shell (SSH).
    * **Skalowanie klastra**: umożliwia toochange hello liczba węzłów procesu roboczego dla tego klastra.
    * **Usuń**: usuwa hello klastra.
    * **Dzienniki aktywności**: Pokaż i zapytania Dzienniki aktywności.
    * **Kontrola (IAM) dostępu**: za pomocą przypisań ról.  Zobacz [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md).
    * **Tagi**: umożliwia możesz tooset klucza i wartości pary toodefine niestandardowych taksonomii usług w chmurze. Na przykład może utworzyć klucz o nazwie **projektu**, a następnie użyć wspólną wartość wszystkie usługi powiązane z określonego projektu.
    * **Diagnozowanie i rozwiązywanie problemów**: Wyświetl informacje dotyczące rozwiązywania problemów.
    * **Blokuje**: Dodaj blokady tooprevent hello klastra jest zmodyfikowany lub usunięty.
    * **Skrypt automatyzacji**: wyświetlanie i eksportowanie szablonu usługi Azure Resource Manager hello hello klastra. Obecnie można wyeksportować tylko hello zależne konto magazynu Azure. Zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Szybki Start**: Wyświetla informacje, który pomoże Ci rozpocząć korzystanie z usługi HDInsight.
    * **Narzędzia HDInsight**: narzędzia powiązane informacje pomocy dla usługi HDInsight.
    * **Klaster logowania**: wyświetlanie informacji o logowaniu klastra hello.
    * **Użycie Core subskrypcji**: Wyświetl hello rdzeni używany i dostępny dla Twojej subskrypcji.
    * **Skalowanie klastra**: Zwiększ i zmniejszenie hello liczba węzłów procesu roboczego w klastrze. Zobacz[skalować klastrów](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: Pokazuje hello instrukcje tooconnect toohello klastra przy użyciu połączenia protokołu Secure Shell (SSH). Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Partnera usługi HDInsight**: Dodaj/Usuń hello bieżącego partnera usługi HDInsight.
    * **Zewnętrzne magazyny**: Wyświetl hello Hive i Oozie magazyny. Magazyny Hello można skonfigurować tylko podczas procesu tworzenia klastra hello. Zobacz [użyć na potrzeby magazynu metadanych Hive/Oozie](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Akcje skryptu**: skrypty Bash uruchomić w klastrze hello. Zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).
    * **Aplikacje**: aplikacje usługi HDInsight dodawania i usuwania.  Zobacz [instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md).
    * **Właściwości**: Wyświetl hello właściwości klastra.
    * **Konta magazynu**: Wyświetl hello kont magazynu i klucze hello. konta magazynu Hello są konfigurowane podczas procesu tworzenia klastra hello.
    * **Tożsamość usługi AAD klastra**:
    * **Nowe żądanie pomocy technicznej**: pozwala toocreate biletu pomocy technicznej o pomoc techniczna firmy Microsoft.
    
6. Kliknij przycisk **właściwości**:

    właściwości Hello są:

   * **Nazwa hosta**: Nazwa klastra.
   * **Adres URL klastra**. Witaj adres URL dla interfejsu sieci web Ambari hello.
   * **Stan**: obejmują zostało przerwane, zaakceptowane, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, operacyjne, uruchomione, błąd, usuwanie, usunięty, upłynął limit czasu, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, ClusterCustomization CertRolloverQueued, ResizeQueued,
   * **Region**: Lokalizacja platformy Azure. Aby uzyskać listę obsługiwanych lokalizacji platformy Azure, zobacz hello **Region** lista rozwijana na [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Data utworzenia**.
   * **System operacyjny**: albo **Windows** lub **Linux**.
   * **Typ**: Hadoop, HBase, Storm, Spark.
   * **Wersja**. Zobacz [wersji usługi HDInsight](hdinsight-component-versioning.md)
   * **Subskrypcja**: Nazwa subskrypcji.
   * **Domyślne źródło danych**: hello domyślnego systemu plików dla klastra.
   * **Rozmiar węzłów procesu roboczego**.
   * **HEAD rozmiaru węzła**.

## <a name="delete-clusters"></a>Usuwanie klastrów
Usunięcie klastra nie powoduje usunięcia hello domyślne konto magazynu lub wszystkie połączone konta magazynu. Można ponownie utworzyć klaster hello przy użyciu hello tego samego konta magazynu i hello tego samego magazyny. Jest zalecana toouse nowego domyślnego kontenera obiektów Blob podczas ponownego tworzenia klastra hello.

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **klastrów usługi HDInsight** z menu po lewej stronie powitania. Jeśli nie widzisz **klastrów usługi HDInsight**, kliknij przycisk **więcej usług** pierwszy.
3. Kliknij klaster hello, które mają toodelete.
4. Kliknij przycisk **usunąć** z hello menu u góry, a następnie wykonaj instrukcje hello.

Zobacz też [Wstrzymaj/zamykania klastrów](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Dodawanie kolejnych kont magazynu

Po utworzeniu klastra można dodać dodatkowych kont usługi Azure Storage i Azure Data Lake Store. Aby uzyskać więcej informacji, zobacz [dodać dodatkowy magazyn kont tooHDInsight](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Skalowanie klastrów
Skalowanie funkcji klastra Hello umożliwia toochange hello liczba węzłów procesu roboczego, używane przez klaster działa w usłudze Azure HDInsight bez konieczności toore — Tworzenie klastra hello.

> [!NOTE]
> Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane. Jeśli masz pewności, jaka wersja hello klastra, można sprawdzić hello stronę właściwości.  Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).
>
>

wpływ Hello Zmienianie hello liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:

* Usługa Hadoop

    Można zwiększyć bezproblemowo hello liczba węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania. W trakcie operacji hello również można przesłać nowe zadania. Błędy w operacji skalowania bezpiecznie obsługi tak, aby hello klastra zawsze pozostanie w stanie funkcjonalności.

    Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby hello węzły danych są ponownie uruchamiane niektórych usług hello hello klastra. To działanie powoduje wszystkich uruchomionych i oczekujących zadań toofail na zakończenie hello hello operacji skalowania. Można jednak Prześlij ponownie hello zadania po zakończeniu operacji hello.
* HBase

    Można bezproblemowo dodać lub usunąć klaster HBase tooyour węzłów, jest uruchomiona. Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia hello operacji skalowania. Można jednak również ręcznie saldo serwerów regionalnych hello po zalogowaniu się headnode toohello klastra i uruchomione hello poniższych poleceń z poziomu okna wiersza polecenia:

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

    ![HDInsight Storm Zrównoważ skali](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Poniżej przedstawiono przykładowy sposób hello toouse interfejsu wiersza polecenia polecenie topologii Storm hello toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**klastry tooscale**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **klastrów usługi HDInsight** z menu po lewej stronie powitania.
3. Kliknij klaster hello ma tooscale.
3. Kliknij przycisk **skalowanie klastra**.
4. Wprowadź **węzłami liczba procesów roboczych**. limit Hello hello liczby węzłów klastra jest zależny od używanej subskrypcji platformy Azure. Możesz skontaktować się rozliczeń limit hello tooincrease pomocy technicznej.  informacje o kosztach Hello odzwierciedla hello zmiany toohello liczba węzłów.

    ![HDInsight hadoop hbase storm spark skali](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Wstrzymaj/zamykania klastrów

Większość zadań usługi Hadoop to zadania wsadowe, które będzie uruchamiane co pewien czas. Większość klastrów platformy Hadoop, istnieje duże okresów czasu hello klastra nie jest używany do przetwarzania. Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany.
Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany. Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane.

Istnieje wiele sposobów można program hello proces:

* Użytkownik fabryki danych Azure. Zobacz [klastrów tworzenie na żądanie opartą na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu fabryki danych Azure](hdinsight-hadoop-create-linux-clusters-adf.md) do tworzenia usługi HDInsight na żądanie połączone usługi.
* Za pomocą programu Azure PowerShell.  Zobacz [analizowanie danych opóźnienie transmitowane](hdinsight-analyze-flight-delay-data.md).
* Za pomocą interfejsu wiersza polecenia platformy Azure. Zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu wiersza polecenia Azure](hdinsight-administer-use-command-line.md).
* Używanie zestawu SDK .NET usługi HDInsight. Zobacz [Hadoop przesyłania zadań](hdinsight-submit-hadoop-jobs-programmatically.md).

Aby hello uzyskać informacje o cenach, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete klastra z hello portalu, zobacz [usuwać klastry](#delete-clusters)


## <a name="upgrade-clusters"></a>Uaktualnij klastrów

Zobacz [HDInsight uaktualnienia klastra tooa nowsza wersja](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Zmienianie haseł
Klaster usługi HDInsight mogą być dwa konta użytkownika. Witaj konta użytkownika klastra usługi HDInsight () Konto użytkownika HTTP) i hello konta użytkownika SSH podczas procesu tworzenia hello są tworzone. Można użyć hello Ambari web UI toochange hello klastra użytkownika nazwa użytkownika konta i hasło hello toochange akcji skryptu konta użytkownika SSH

### <a name="change-hello-cluster-user-password"></a>Zmień hasło użytkownika klastra hello
Można użyć hasła użytkownika hello Interfejsu sieci Web Ambari toochange hello klastra. toolog w tooAmbari, należy użyć hello istniejącego klastra użytkownika i hasło.

> [!NOTE]
> Zmiany hasła użytkownika (Administrator) klastra hello może spowodować skryptu, który akcje przeprowadzony na toofail tego klastra. Jeśli masz żadnych akcji utrwalonego skryptu, które odnoszą się do węzłów procesu roboczego te skrypty może zakończyć się niepowodzeniem podczas dodawania węzłów klastra toohello za pomocą operacji zmiany rozmiaru. Aby uzyskać więcej informacji dotyczących akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Zaloguj się przy użyciu interfejsu użytkownika sieci Web Ambari toohello hello poświadczenia użytkownika klastra usługi HDInsight. Witaj domyślna nazwa użytkownika to **admin**. hello adres URL jest **https://&lt;nazwy klastra usługi HDInsight > azurehdinsight.net**.
2. Kliknij przycisk **Admin** z hello menu u góry, a następnie kliknij pozycję "Zarządzaj Ambari".
3. W menu po lewej stronie powitania kliknij **użytkowników**.
4. Kliknij przycisk **Admin**.
5. Kliknij przycisk **zmiany hasła**.

Ambari następnie zmiany hasła hello we wszystkich węzłach w klastrze hello.

### <a name="change-hello-ssh-user-password"></a>Zmienianie hasła użytkownika SSH hello
1. Za pomocą edytora tekstu, zapisywanie hello następującego tekstu w pliku o nazwie **changepassword.sh**.

   > [!IMPORTANT]
   > Należy użyć edytora używającą LF jako hello zakończenia wiersza. Jeśli Edytor hello używa CRLF, hello skrypt nie działa.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Przekazywanie hello tooa lokalizacji przechowywania plików, które są dostępne z usługi HDInsight przy użyciu adresu HTTP lub HTTPS. Na przykład plik publicznego przechowywać takie jak magazyn OneDrive lub obiektów Blob platformy Azure. Zapisz plik toohello identyfikatora URI (adres HTTP lub HTTPS) hello, ten identyfikator URI jest w miarę potrzeb hello następnego kroku.
3. Witaj portalu Azure kliknij **klastrów usługi HDInsight**.
4. Kliknij przycisk z klastrem usługi HDInsight.
4. Kliknij przycisk **skryptu akcji**.
4. Z hello **akcji skryptu** bloku, wybierz opcję **przesłać nowe**. Gdy hello **przesłać akcji skryptu** zostanie wyświetlony blok, wprowadź hello następujących informacji:

   | Pole | Wartość |
   | --- | --- |
   | Nazwa |Zmień ssh hasło |
   | Skrypt bash identyfikatora URI |Witaj URI toohello changepassword.sh pliku |
   | Węzły (Head, proces roboczy, Nimbus, przełożonego, dozorcy itp.) |✓ dla wszystkich typów węzła na liście |
   | Parametry |Wprowadź nazwę użytkownika SSH hello, a następnie hello nowe hasło. Powinien istnieć jeden odstęp między hello nazwy użytkownika i hasła hello. |
   | Utrwal tę akcję skryptu... |Nie zaznaczaj tego pola wyboru. |
5. Wybierz **Utwórz** tooapply hello skryptu. Po zakończeniu działania skryptu hello, jest możliwe tooconnect toohello klastra przy użyciu protokołu SSH z hello nowe hasło.

## <a name="grantrevoke-access"></a>Dostęp do przydzielenia/odwołania
Klastry HDInsight są powitania po HTTP usługi sieci web (wszystkie te usługi mają RESTful punkty końcowe):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Domyślnie te usługi są przyznawane dostępu. Użytkownik może revoke/grant hello dostępu przy użyciu [interfejsu wiersza polecenia Azure](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) i [programu Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Znajdź hello identyfikator subskrypcji

**toofind identyfikatorów subskrypcji platformy Azure**

1. Zaloguj się toohello [Portal][azure-portal].
2. Kliknij przycisk **subskrypcje**. Każda subskrypcja ma nazwę i identyfikator.

Każdy klaster jest wiązana tooan subskrypcji platformy Azure. Witaj subskrypcji identyfikator jest wyświetlany w klastrze hello **podstawowych** kafelka. Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Znajdź hello grupy zasobów
W trybie Azure Resource Manager hello każdego klastra usługi HDInsight jest tworzony z grupy usługi Azure Resource Manager. Grupa usługi Resource Manager Hello klastra należy tooappears w:

* Lista klastrów Hello ma **grupy zasobów** kolumny.
* Klaster **podstawowych** kafelka.  

Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Znajdź hello domyślne konto magazynu
Każdy klaster usługi HDInsight ma domyślne konto magazynu. Witaj domyślne konto magazynu i kluczy dla klastra jest wyświetlana w obszarze **kont magazynu**. Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Uruchamianie zapytań Hive
Nie można uruchomić zadania Hive bezpośrednio z hello portalu Azure, ale może użyć hello Hive widoku sieci Web Ambari w interfejsie użytkownika.

**toorun zapytań Hive przy użyciu widoku Hive narzędzia Ambari**

1. Zaloguj się przy użyciu interfejsu użytkownika sieci Web Ambari toohello hello poświadczenia użytkownika klastra usługi HDInsight. Witaj domyślna nazwa użytkownika to **admin**. hello adres URL jest **https://&lt;nazwy klastra usługi HDInsight > azurehdinsight.net**.
2. Otwórz widok Hive, jak pokazano w powitania po zrzut ekranu:  

    ![HDInsight hive widoku](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Kliknij przycisk **zapytania** z górnego menu hello.
4. Wprowadź zapytanie Hive w **edytora zapytań**, a następnie kliknij przycisk **Execute**.

## <a name="monitor-jobs"></a>Monitorowanie zadań
Zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari hello](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Przeglądanie plików
Witaj portalu Azure można przeglądać zawartość hello hello domyślnego kontenera.

1. Zaloguj się za[https://portal.azure.com](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** z hello toolist menu po lewej stronie hello istniejących klastrów.
3. Kliknij nazwę klastra hello. Jeśli lista klastrów hello jest długa, można użyć filtru u góry hello hello strony.
4. Kliknij przycisk **kont magazynu** z menu po lewej stronie powitania klastra.
5. Kliknij konto magazynu.
7. Kliknij przycisk hello **obiekty BLOB** kafelka.
8. Kliknij nazwę kontenera domyślnego hello.

## <a name="monitor-cluster-usage"></a>Monitorowanie użycia klastra
Witaj **użycia** części bloku klastra usługi HDInsight hello Wyświetla informacje o hello liczba rdzeni tooyour dostępnych subskrypcji do użycia z usługą HDInsight, a także hello liczba rdzeni przydzielone toothis klastra i sposób ich przydzielone dla węzłów hello w tym klastrze. Zobacz [klastrów listy i Pokaż](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello usługi świadczone przez hello klastra usługi HDInsight, należy użyć narzędzia Ambari Web lub hello interfejsu API REST Ambari. Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Połącz tooa klastra

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [Używanie protokołu SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Następne kroki
W tym artykule uzyskanych niektóre funkcje administracyjne podstawowe. toolearn więcej, zobacz następujące artykuły hello:

* [Administrowanie HDInsight przy użyciu programu Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia platformy Azure](hdinsight-administer-use-command-line.md)
* [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Korzystanie z programu Hive w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig w usłudze HDInsight](hdinsight-use-pig.md)
* [Użyj Sqoop w usłudze HDInsight](hdinsight-use-sqoop.md)
* [Rozpoczynanie pracy z usługą Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Jest wersję platformy Hadoop w usłudze Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Wiersz polecenia usługi Hadoop"
