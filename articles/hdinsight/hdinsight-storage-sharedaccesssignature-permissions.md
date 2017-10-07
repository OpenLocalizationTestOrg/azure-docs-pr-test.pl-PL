---
title: "aaaRestrict dostępu przy użyciu sygnatury dostępu współdzielonego - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse sygnatury dostępu współdzielonego toorestrict HDInsight dostępu toodata przechowywane w obiektach blob magazynu Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Użyj toodata dostępu toorestrict sygnatury dostępu współdzielonego magazynu Azure w usłudze HDInsight

HDInsight ma pełny dostęp toodata na kontach magazynu Azure hello skojarzony z klastrem hello. Możesz użyć sygnatury dostępu współdzielonego w hello obiektów blob kontenera toorestrict dostępu toohello danych. Na przykład tooprovide dostęp tylko do odczytu toohello danych. Udostępniony sygnatur dostępu (SAS) są funkcją kontami magazynu Azure, umożliwiający toolimit toodata dostępu. Na przykład dostarczanie toodata dostęp tylko do odczytu.

> [!IMPORTANT]
> Jako rozwiązanie przy użyciu Apache zakres należy rozważyć użycie HDInsight przyłączonych do domeny. Aby uzyskać więcej informacji, zobacz hello [HDInsight przyłączonych do domeny skonfiguruj](hdinsight-domain-joined-configure.md) dokumentu.

> [!WARNING]
> HDInsight musi mieć pełny dostęp toohello domyślny magazyn dla klastra hello.

## <a name="requirements"></a>Wymagania

* Subskrypcja platformy Azure
* C# lub języka Python. Przykład kodu C# stanowi rozwiązanie Visual Studio.

  * Visual Studio musi być w wersji 2013, 2015 lub 2017
  * Python musi być w wersji 2.7 lub wyższej

* Klaster usługi HDInsight opartej na systemie Linux lub [programu Azure PowerShell] [ powershell] — Jeśli masz istniejący klaster opartych na systemie Linux, można użyć narzędzia Ambari tooadd klastra toohello sygnatura dostępu współdzielonego. Jeśli nie, można użyć programu Azure PowerShell toocreate klastra i dodać sygnaturę dostępu współdzielonego podczas tworzenia klastra.

    > [!IMPORTANT]
    > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Witaj przykładowe pliki z [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). To repozytorium zawiera hello następujące elementy:

  * Projektu programu Visual Studio, który można utworzyć kontenera magazynu, zapisane zasady i skojarzenia zabezpieczeń do użycia z usługą HDInsight
  * Skrypt w języku Python, który można utworzyć kontenera magazynu, zapisane zasady i skojarzenia zabezpieczeń do użycia z usługą HDInsight
  * Skrypt programu PowerShell, który może tworzyć HDInsight klastra i skonfigurować go toouse hello SAS.

## <a name="shared-access-signatures"></a>Sygnatury dostępu współdzielonego

Istnieją dwa rodzaje sygnatur dostępu współdzielonego:

* Ad hoc: uprawnienia dla hello SAS są określone na powitania identyfikatora URI połączenia SAS, czas wygaśnięcia i godzina rozpoczęcia hello.

* Przechowywane zasad dostępu: zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobów, takich jak kontenera obiektów blob. Zasady mogą być używane toomanage ograniczenia dla co najmniej jeden sygnatur dostępu współdzielonego. Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, hello SAS dziedziczy ograniczenia hello — uprawnienia - zdefiniowane zasady dostępu hello przechowywane, czas wygaśnięcia i godzina rozpoczęcia hello.

Witaj różnica pomiędzy formularzami Witaj dwie ważne jest jeden scenariusz klucza: odwołania. Sygnatury dostępu Współdzielonego jest adres URL, więc każdy, kto uzyskuje hello SAS może być używany, niezależnie od tego, kto go zażądało toobegin z. Sygnatury dostępu Współdzielonego zostanie opublikowana publicznie, może służyć każdy hello world. Sygnatury dostępu Współdzielonego, który jest rozpowszechniany jest prawidłowy, dopóki jedna z następujących czterech zdarzeń sytuacji:

1. czas wygaśnięcia Hello określony na powitania osiągnięty sygnatury dostępu Współdzielonego.

2. czas wygaśnięcia Hello określone zasady dostępu hello przechowywane odwołuje się hello osiągnięty sygnatury dostępu Współdzielonego. Witaj następujące scenariusze spowodować czas wygaśnięcia hello toobe osiągnięto:

    * Upłynął czas Hello.
    * zasady dostępu Hello przechowywane jest zmodyfikowany toohave czas wygaśnięcia w przeszłości hello. Zmiana czasu wygaśnięcia hello jest hello toorevoke jednokierunkowych SAS.

3. Witaj przechowywane odwołuje hello SAS jest usuwane, który jest inny sposób hello toorevoke SAS zasad dostępu. Jeśli ponownego tworzenia zasad dostępu hello przechowywane z hello takie same nazwy, wszystkie tokeny sygnatury dostępu Współdzielonego dla poprzednich zasad hello są prawidłowe, (Jeśli czas wygaśnięcia hello na powitania nie przeszło SAS). Jeśli planujesz hello toorevoke sygnatury dostępu Współdzielonego, można toouse się, że inną nazwę Jeśli ponownego tworzenia zasad dostępu hello z upływem czasu w przyszłości hello.

4. ponownego wygenerowania klucza konta Hello, który był używany toocreate hello SAS. Trwa ponowne generowanie klucza hello powoduje, że wszystkie aplikacje używające hello poprzedniego klucza toofail uwierzytelniania. Zaktualizuj wszystkie składniki toohello nowego klucza.

> [!IMPORTANT]
> Identyfikator URI sygnatury dostępu współdzielonego jest skojarzony z sygnaturą hello klucza toocreate używane konto hello i hello skojarzonych zasad dostępu przechowywanych (jeśli istnieje). Jeśli określono żadnych zasad dostępu przechowywane, hello tylko sposób toorevoke sygnatury dostępu współdzielonego jest klucz konta hello toochange.

Firma Microsoft zaleca zawsze używać zasad dostępu przechowywane. Podczas korzystania z zasady przechowywane, możesz odwołać podpisów lub przedłużyć datę wygaśnięcia hello, zgodnie z potrzebami. kroki Hello w tym dokumencie Użyj toogenerate zasady dostępu do przechowywanych sygnatury dostępu Współdzielonego.

Aby uzyskać więcej informacji dotyczących sygnatur dostępu współdzielonego, zobacz [modelu sygnatur dostępu Współdzielonego hello opis](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Tworzenie zasad przechowywane i sygnatury dostępu Współdzielonego, za pomocą C\#

1. Otwórz rozwiązanie hello w programie Visual Studio.

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SASToken** projekt i wybierz **właściwości**.

3. Wybierz **ustawienia** i Dodaj wartości hello następujące wpisy:

   * StorageConnectionString: hello parametrów połączenia dla konta magazynu hello, które mają toocreate zapisane zasady i sygnatury dostępu Współdzielonego dla. powinna mieć ona Hello format `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` gdzie `myaccount` hello nazwa konta magazynu i `mykey` jest hello klucza dla konta magazynu hello.

   * ContainerName: hello kontenera na koncie magazynu hello, który ma dostęp toorestrict do.

   * SASPolicyName: hello toouse nazwy dla hello przechowywane toocreate zasad.

   * FileToUpload: hello ścieżka tooa pliku, który jest kontenerem toohello przekazane.

4. Uruchom projekt hello. Po wygenerowaniu hello SAS, wyświetlane są toohello podobne informacje następującego tekstu:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Zapisz token zasady sygnatury dostępu Współdzielonego hello, nazwa konta magazynu i nazwy kontenera. Te wartości są używane podczas kojarzenia hello konta magazynu z klastra usługi HDInsight.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Tworzenie zasad przechowywane i SAS używany język Python

1. Otwórz plik SASToken.py hello i zmienić hello następujące wartości:

   * zasady\_name: hello toouse nazwy dla hello przechowywane toocreate zasad.

   * Magazyn\_konta\_name: hello nazwę konta magazynu.

   * Magazyn\_konta\_klucz: hello klucza dla konta magazynu hello.

   * Magazyn\_kontenera\_name: hello kontenera na koncie magazynu hello, który ma dostęp toorestrict do.

   * przykład\_pliku\_ścieżki: hello ścieżka tooa pliku, który jest kontenerem toohello przekazane.

2. Uruchom skrypt hello. Wyświetla hello SAS tokenu podobne toohello następującego tekstu po ukończeniu działania skryptu hello:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Zapisz token zasady sygnatury dostępu Współdzielonego hello, nazwa konta magazynu i nazwy kontenera. Te wartości są używane podczas kojarzenia hello konta magazynu z klastra usługi HDInsight.

## <a name="use-hello-sas-with-hdinsight"></a>Użyj hello SAS z usługą HDInsight

Podczas tworzenia klastra usługi HDInsight, należy określić konto magazynu głównego i opcjonalnie możesz określić dodatkowe konta magazynu. Obie te metody dodawania magazynu wymagają konta magazynu toohello pełny dostęp i kontenerów, które są używane.

toouse kontener tooa dostępu toolimit sygnatura dostępu współdzielonego, Dodaj toohello wpisu niestandardowego **lokacji podstawowej** konfiguracji hello klastra.

* Aby uzyskać **opartych na systemie Windows** lub **opartych na systemie Linux** klastrów usługi HDInsight, można dodać wpisu hello podczas tworzenia klastra przy użyciu programu PowerShell.
* Aby uzyskać **opartych na systemie Linux** klastrów usługi HDInsight, zmień konfigurację powitania po utworzeniu klastra przy użyciu narzędzia Ambari.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Tworzenie klastra, który wykorzystuje hello SAS

Przykład tworzenia klastra usługi HDInsight tego hello używa SAS jest uwzględniona w hello `CreateCluster` katalogu hello repozytorium. toouse, który go hello Użyj następujących kroków:

1. Otwórz hello `CreateCluster\HDInsightSAS.ps1` plik w edytorze tekstu i zmodyfikuj hello następujące wartości na początku hello hello dokumentu.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Na przykład zmienić `'mycluster'` toohello nazwy klastra hello ma toocreate. wartości SAS Hello powinna odpowiadać wartości hello z poprzednich kroków hello podczas tworzenia konta magazynu i tokenu sygnatury dostępu Współdzielonego.

    Po zmianie wartości hello, Zapisz plik hello.

2. Otwórz nowy wiersz programu Azure PowerShell. Jeśli masz doświadczenia w pracy z programem Azure PowerShell lub nie został zainstalowany, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell][powershell].

1. W wierszu hello Użyj hello następujące polecenie tooyour tooauthenticate subskrypcji platformy Azure:

    ```powershell
    Login-AzureRmAccount
    ```

    Po wyświetleniu monitu zaloguj się za pomocą hello konta dla subskrypcji platformy Azure.

    Jeśli konto jest skojarzone z wieloma subskrypcjami platformy Azure, może być konieczne toouse `Select-AzureRmSubscription` tooselect hello subskrypcji chcesz toouse.

4. W wierszu hello Zmień katalogi toohello `CreateCluster` katalog zawierający plik HDInsightSAS.ps1 hello. Następnie użyj następującego skryptu hello toorun polecenia hello

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Jako hello skrypt będzie uruchamiany rejestruje wierszu polecenia programu PowerShell toohello danych wyjściowych podczas tworzenia zasobu hello konta grupy i magazynu. Jesteś użytkownikiem hello HTTP zostanie wyświetlony monit o tooenter hello klastra usługi HDInsight. To konto jest używane toosecure protokołu HTTP/s dostępu toohello klastra.

    W przypadku tworzenia opartych na systemie Linux klaster, zostanie wyświetlony monit o nazwę konta użytkownika SSH i hasło. To konto jest używane tooremotely dziennika w klastrze toohello.

   > [!IMPORTANT]
   > Po wyświetleniu monitu o hello protokołu HTTP/s lub SSH nazwy użytkownika i hasła, należy podać hasło, które spełnia następujące kryteria hello:
   >
   > * Musi być co najmniej 10 znaków
   > * Musi zawierać co najmniej jedną cyfrę
   > * Musi zawierać co najmniej jeden znak inny niż alfanumeryczny
   > * Musi zawierać co najmniej jedną wielką lub małą literę

Trwa trochę czasu toocomplete tego skryptu, zazwyczaj około 15 minut. Po zakończeniu hello skryptu bez żadnych błędów, hello klaster został utworzony.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Użyj hello SAS z istniejącego klastra

Jeśli masz istniejący klaster opartych na systemie Linux, można dodać hello SAS toohello **lokacji podstawowej** konfiguracji przy użyciu hello następujące kroki:

1. Otwórz hello Ambari web UI dla klastra. adres Hello na tej stronie jest https://YOURCLUSTERNAME.azurehdinsight.net. Po wyświetleniu monitu uwierzytelniania toohello klastra przy użyciu nazwy administratora hello (Administrator) i hasło użyte podczas tworzenia klastra hello.

2. Hello po lewej stronie powitania interfejsu użytkownika sieci web Ambari, zaznacz **HDFS** , a następnie wybierz hello **Configs** kartę w środku hello hello strony.

3. Wybierz hello **zaawansowane** , a następnie przewiń do momentu znalezienia hello **niestandardowe core-site** sekcji.

4. Rozwiń węzeł hello **niestandardowe core-site** sekcji, a następnie przewijania zakończenia toohello i wybierz hello **Dodaj właściwość... ** łącza. Użyj następujących hello wartości hello **klucza** i **wartość** pola:

   * **Klucz**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Wartość**: hello SAS zwrócony przez hello aplikacji C# lub Python został przeprowadzony wcześniej

     Zastąp **CONTAINERNAME** o nazwie kontenera hello używane z aplikacji hello C# lub SAS. Zastąp **STORAGEACCOUNTNAME** nazwy konta magazynu hello używane.

5. Kliknij przycisk hello **Dodaj** przycisk toosave tego klucza i wartości, a następnie kliknij przycisk hello **zapisać** przycisk zmiany konfiguracji hello toosave. Po wyświetleniu monitu, Dodaj opis zmian hello ("Dodawanie dostępu do pamięci masowej SAS" na przykład), a następnie kliknij przycisk **zapisać**.

    Kliknij przycisk **OK** kiedy hello zmiany zostały ukończone.

   > [!IMPORTANT]
   > Przed hello zmiany zostały uwzględnione, należy ponownie uruchomić kilka usług.

6. W sieci web Ambari hello interfejsu użytkownika, wybierz **HDFS** liście hello na powitania po lewej, a następnie wybierz **Uruchom ponownie wszystkie** z hello **akcji usługi** listy rozwijanej listy na powitania prawo. Po wyświetleniu monitu wybierz **Włącz tryb konserwacji** , a następnie uruchom ponownie wszystkie __Conform select ".

    Powtórz ten proces dla MapReduce2 i YARN.

7. Po ponownym uruchomieniu usługi hello, wybierz każdego z nich i Wyłącz tryb konserwacji z hello **akcji usługi** listy rozwijanej.

## <a name="test-restricted-access"></a>Testowanie dostęp ograniczony

tooverify ograniczono dostępu, użyj hello następujące metody:

* Aby uzyskać **opartych na systemie Windows** klastrów usługi HDInsight, użyj klastra toohello tooconnect pulpitu zdalnego. Aby uzyskać więcej informacji, zobacz [połączyć za pomocą protokołu RDP tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Po nawiązaniu połączenia użyj hello **Hadoop wiersza polecenia** ikonę na powitania pulpitu tooopen wiersz polecenia.

* Aby uzyskać **opartych na systemie Linux** klastrów usługi HDInsight, użyj klastra toohello tooconnect SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Po nawiązaniu połączenia toohello klastra, użyj hello następujące możliwe tylko odczyt i listy elementów na koncie magazynu SAS hello tooverify kroki:

1. zawartość hello toolist hello kontenera, hello Użyj następującego polecenia w wierszu hello: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Zastąp **SASCONTAINER** o nazwie hello kontenera hello utworzone dla hello sygnatury dostępu Współdzielonego konta magazynu. Zastąp **SASACCOUNTNAME** o nazwie hello hello konto magazynu dla hello sygnatury dostępu Współdzielonego.

    Lista Hello zawiera plik hello przekazane po utworzenia kontenera hello i skojarzenia zabezpieczeń.

2. Użyj hello następujące polecenie tooverify przeczytanie hello zawartość pliku hello. Zastąp hello **SASCONTAINER** i **SASACCOUNTNAME** jak hello w poprzednim kroku. Zastąp **FILENAME** hello nazwą pliku hello wyświetlane w hello poprzednie polecenie:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    To polecenie wyświetla zawartość hello hello pliku.

3. Witaj Użyj następującego polecenia toodownload hello pliku toohello lokalnego systemu plików:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    To polecenie pliki do pobrania hello tooa lokalnego pliku o nazwie **plik_testowy.txt**.

4. Użyj hello następujące polecenie tooupload hello pliku lokalnego tooa nowy plik o nazwie **testupload.txt** na powitania pamięci masowej SAS:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Pojawi się komunikat toohello podobne, następującego tekstu:

        put: java.io.IOException

    Ten błąd występuje, ponieważ lokalizacja przechowywania hello jest odczytu + tylko z listy. Witaj Użyj następującego polecenia tooput hello danych na hello domyślny magazyn dla klastra hello, który jest dostępny do zapisu:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    Ten czas operacji hello powinno zakończyć się pomyślnie.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="a-task-was-canceled"></a>Zadanie zostało anulowane

**Objawy**: podczas tworzenia klastra za pomocą skryptu PowerShell hello, może zostać wyświetlony następujący komunikat o błędzie hello:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Przyczyna**: ten błąd może wystąpić, jeśli używasz hasła dla użytkownika administracyjnego/HTTP hello hello klastra lub (w przypadku klastrów z systemem Linux) hello użytkownika SSH.

**Rozdzielczość**: Użyj hasła spełniającego hello następujące kryteria:

* Musi być co najmniej 10 znaków
* Musi zawierać co najmniej jedną cyfrę
* Musi zawierać co najmniej jeden znak inny niż alfanumeryczny
* Musi zawierać co najmniej jedną wielką lub małą literę

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już jak tooadd tooyour ograniczony dostęp do magazynu klastra usługi HDInsight, Dowiedz się inne sposoby toowork z danymi w klastrze:

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
