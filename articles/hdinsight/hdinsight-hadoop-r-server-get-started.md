---
title: "aaaGet wprowadzenie R Server w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się jak toocreate Apache Spark w klastrze usługi HDInsight, która obejmuje R Server i przesłać skrypt języka R w klastrze hello."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Wprowadzenie do korzystania z oprogramowania R Server w usłudze HDInsight

HDInsight obejmuje toobe opcji R Server zintegrowana z klastrem usługi HDInsight. Ta opcja umożliwia skrypty R toouse Spark i MapReduce toorun rozproszone obliczenia. W tym dokumencie możesz dowiedzieć się, jak toocreate R Server w klastrze usługi HDInsight, a następnie uruchom R skrypt, który demonstruje użycie platforma Spark dla rozproszone obliczenia R.


## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**: przed rozpoczęciem tego samouczka musisz mieć subskrypcję platformy Azure. Artykuł Przejdź toohello [bezpłatna wersja próbna platformy Microsoft Azure Pobierz](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) Aby uzyskać więcej informacji.
* **Klient Secure Shell (SSH)**: jest używany przez klienta SSH tooremotely Połącz z klastrem usługi HDInsight toohello i Uruchom polecenia bezpośrednio w klastrze hello. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
* **(Opcjonalnie) kluczy SSH**: można zabezpieczyć hello SSH użyte konto tooconnect toohello klastra przy użyciu hasła lub klucza publicznego. Przy użyciu hasła jest łatwiejsze i umożliwia tooget można uruchomić bez konieczności toocreate pary kluczy publiczny/prywatny. Jednak użycie klucza jest bezpieczniejsze.

> [!NOTE]
> Hello kroków w tym dokumencie założono, że używasz hasła.


## <a name="automated-cluster-creation"></a>Zautomatyzowane tworzenie klastra

Można zautomatyzować tworzenie hello serwerów R HDInsight za pomocą usługi Azure Resource Manager szablony, hello zestawu SDK, a także programu PowerShell.

* Zobacz toocreate R Server przy użyciu szablonu usługi Azure Resource Management [wdrażanie klastra usługi HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* Zobacz toocreate moduł R Server przy użyciu zestawu .NET SDK hello [tworzenia opartych na systemie Linux klastrów w usłudze HDInsight przy użyciu zestawu .NET SDK hello.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R Server przy użyciu programu powershell, zobacz artykuł hello na [Tworzenie serwera R w usłudze HDInsight przy użyciu programu PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Tworzenie klastra hello przy użyciu hello portalu Azure

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Wybierz pozycję **Nowy** -> **Rozwiązania inteligentne + analiza** -> **HDInsight**.

    ![Obraz tworzenia nowego klastra](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. W hello **szybkie tworzenie** uruchomienia systemu, wprowadź nazwę klastra hello w hello **nazwy klastra** pola. Jeśli masz wiele subskrypcji Azure, użyj hello **subskrypcji** wpis tooselect hello jedną ma toouse.

    ![Wybór nazwy klastra i subskrypcji](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Wybierz **typ klastra** tooopen hello **konfiguracji klastra** bloku. Na powitania **konfiguracji klastra** bloku hello wybierz następujące opcje:

    * **Typ klastra**: R Server
    * **Wersja**: hello wybierz wersję tooinstall R Server w klastrze hello. Witaj obecnie dostępna jest wersja ***R Server 9.1 (3,6 HDI)***. Dostępne są informacje o wersji dla hello dostępne wersje R Server [tutaj](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **R Studio community edition dla R Server**: IDE tej przeglądarki jest instalowany domyślnie na powitania węzła krawędzi. Jeśli wolisz toonot jest zainstalowany, a następnie usuń zaznaczenie pola wyboru hello. Jeśli wybierzesz toohave ją zainstalować, adres URL hello dla uzyskiwania dostępu do powitalne logowanie do serwera programu RStudio znajduje się w bloku portalu aplikacji dla klastra, po jego utworzeniu.
    * Pozostaw hello inne opcje na powitania wartości domyślne i użyć hello **wybierz** toosave hello klastra typ przycisku.

        ![Zrzut ekranu bloku typu klastra](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Podaj wartości w pozycjach **Nazwa użytkownika logowania klastra** i **Hasło logowania klastra**.

    Określ wartość w pozycji **Nazwa użytkownika SSH**. SSH jest używane tooremotely połączyć toohello klastra przy użyciu **Secure Shell (SSH)** klienta. Można określić użytkownika SSH hello w tym oknie dialogowym lub po utworzeniu klastra hello (na karcie Konfiguracja hello hello klastra). R Server jest skonfigurowany tooexpect **nazwy użytkownika SSH** z "remoteuser".  **Jeśli używasz innej nazwy użytkownika, należy wykonać dodatkowy krok po utworzeniu klastra hello.**

    Pozostaw pole hello sprawdzane pod kątem **Użyj tego samego hasła jak logowania do klastra** toouse **hasło** wpisywania hello uwierzytelniania, jeśli wolisz użycie klucza publicznego.  Należy tooaccess pary kluczy publiczny/prywatny R Server w klastrze hello za pomocą zdalnego klienta jako, na przykład RTVS, programu RStudio lub innego pulpitu IDE. Jeśli zainstalujesz powitania serwera programu RStudio community edition należy toochoose hasło SSH.     

    toocreate i użyj pary kluczy publiczny/prywatny, usuń zaznaczenie pola wyboru **Użyj tego samego hasła jak logowania do klastra** , a następnie wybierz **klucz PUBLICZNY** i wykonać następujące czynności. W poniższych instrukcjach przyjęto, że jest zainstalowane środowisko Cygwin z programem ssh-keygen lub równoważnym.

    * Generowanie pary kluczy publiczny/prywatny z wiersza polecenia hello na laptopie:

        ssh-keygen -t rsa -b 2048

    * Wykonaj hello monitu tooname plik klucza, a następnie wprowadź hasło zwiększyć bezpieczeństwo. Na ekranie powinna przypominać powitania po obrazu:

        ![Wiersz polecenia SSH w systemie Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * To polecenie tworzy plik klucza prywatnego i plik klucza publicznego w obszarze .pub nazwa < prywatny klucz nazwa_pliku > Witaj, na przykład furiosa i furiosa.pub.

        ![Katalog polecenia SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Następnie określ hello pliku klucza publicznego (&#42;. pub) podczas przypisywania HDI klastra poświadczeń i ostatecznie potwierdzić grupy zasobów i region oraz wybierz **dalej**.

        ![Blok poświadczeń](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Zmień uprawnienia na powitania keyfile prywatnych na komputerze przenośnym:

        chmod 600 <nazwa-pliku-klucza-prywatnego>

   * Użyj pliku klucza prywatnego hello przy użyciu protokołu SSH do logowania zdalnego:

        ssh –i <nazwa-pliku-klucza-prywatnego> remoteuser@<hostname public ip>

      Lub, jako części definicji hello programu Hadoop Spark obliczeniowe kontekstu R serwera na powitania klienta. Zobacz hello **przy użyciu Microsoft R Server jako klienta usługi Hadoop** podsekcji w [utworzyć kontekst obliczeniowe platformy Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Witaj szybkie tworzenie przejściach toohello **magazynu** bloku tooselect hello konta magazynu toobe ustawienia używane do lokalizacji głównej hello hello systemu, używane przez klaster hello plików HDFS. Wybierz nowe lub istniejące konto usługi Azure Storage lub istniejące konto usługi Data Lake Storage.

    - W przypadku wybrania konta usługi Azure Storage istniejącego konta magazynu jest zaznaczone, wybierając **wybierz konto magazynu** i wybierając hello odpowiedniego konta. Utwórz nowe konto, przy użyciu hello **Utwórz nowy** łącze w hello **wybierz konto magazynu** sekcji.

      > [!NOTE]
      > W przypadku wybrania **nowy** należy wprowadzić nazwę hello nowe konto magazynu. Zielonego znacznika wyboru jest wyświetlane, gdy nazwa hello jest akceptowany.

      Witaj **domyślny kontener** domyślne nazwy toohello hello klastra. Pozostaw to ustawienie domyślne wartości hello.

      Jeśli wybrano opcji nowego konta magazynu monitu tooselect **lokalizacji** jest podany tooselect które toocreate region hello konta magazynu.  

         ![Blok źródła danych](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Wybieranie lokalizacji hello hello domyślne źródło danych również Ustawia lokalizację hello hello klastra usługi HDInsight. Witaj klaster i domyślne źródło danych musi być w hello tego samego regionu.

    - Chcąc toouse istniejącej usługi Data Lake Store, następnie wybierz hello toouse konta magazynu ADLS i Dodaj klaster hello *Dodaj* tożsamości tooyour klastra tooallow dostępu toohello magazynu. Aby uzyskać więcej informacji na temat tego procesu, zobacz [Tworzenie klastra HDInsight z usługą Data Lake Store za pomocą witryny Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Użyj hello **wybierz** konfiguracji źródła danych hello toosave przycisku.


7. Witaj **Podsumowanie** bloku następnie wyświetla toovalidate wszystkie ustawienia. W tym miejscu możesz zmienić Twojego **rozmiar klastra** toomodify hello liczby serwerów w klastrze, a także określić dowolną **skryptu akcje** ma toorun. Jeśli nie wiadomo, że należy większego klastra, pozostaw hello liczba węzłów procesu roboczego domyślną hello `4`. Hello szacuje się, że koszt klastra hello jest wyświetlane w bloku hello.

    ![podsumowanie klastra](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > W razie potrzeby można zmienić rozmiar klastra później za pomocą hello Portal (**klastra** -> **ustawienia** -> **klaster w skali**) tooincrease lub Zmniejsz hello liczba węzłów procesu roboczego.  Ta zmiana rozmiaru mogą być przydatne, biegu dół klastra hello nieużywane lub Dodawanie wymagań hello toomeet wydajności większych zadań.
   >
   >

   Pewne czynniki tookeep pod uwagę podczas określania rozmiaru sieci klastra, hello węzły danych i węzłem krawędzi hello obejmują:  

   * wydajności Hello rozproszonej analiz R Server w Spark jest proporcjonalny toohello liczba węzłów procesu roboczego po hello danych jest duży.  

   * wydajności Hello R serwera analiz jest liniowa hello rozmiar danych analizowany. Na przykład:  

     * W przypadku małych toomodest danych wydajności jest najlepiej, gdy przeanalizowany w kontekście lokalnym na powitania węzła krawędzi.  Aby uzyskać więcej informacji na hello scenariuszy, w jakich lokalne powitania i Spark obliczeniowe kontekstów najlepiej, zobacz Opcje kontekstu obliczeń platformy R Server w usłudze HDInsight.<br>
     * Jeśli Zaloguj się w węźle krawędzi toohello i uruchom skrypt R, a następnie wykonywane są wszystkie, oprócz hello ScaleR rx — funkcje <strong>lokalnie</strong> na powitania węzła krawędzi. Dlatego hello pamięci i liczby rdzeni węzła krawędzi hello należy ustalać w związku z tym. Witaj, którego dotyczy to również użycie R Server dla HDI kontekst zdalnego obliczeń z komputera przenośnego.

     ![Blok warstw cenowych węzła](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Użyj hello **wybierz** węzła hello toosave przycisk cennik konfiguracji.

   Dostępny jest również link **Pobierz szablon i parametry**. Kliknięcie tego skryptów toodisplay łącza, które mogą być używane tooautomate hello tworzenia klastra z hello wybranej konfiguracji. Skrypty te są także dostępne w hello Azure portalu wpis dla klastra, po jego utworzeniu.

   > [!NOTE]
   > Trwa trochę czasu, zanim toobe klastra hello utworzona, zwykle około 20 minut. Użyj kafelka hello na powitania tablicy startowej lub hello **powiadomienia** wpis na powitania rogu toocheck strony hello na powitania procesu tworzenia.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Połącz tooRStudio serwera

Jeśli wybrano tooinclude serwera programu RStudio community edition w instalacji, możesz uzyskać dostęp hello programu RStudio logowania za pomocą dwóch różnych metod.

1. Przejdź toohello następującego adresu URL (gdzie **CLUSTERNAME** jest nazwą powitania po utworzeniu klastra hello):

    https://**NAZWA-KLASTRA**.azurehdinsight.net/rstudio/

2. Otwórz pozycję hello klastra w hello portalu Azure, wybierz hello **pulpity nawigacyjne serwera R** szybkie łącze, a następnie wybierając hello **pulpitu nawigacyjnego Studio R**:

     ![Pulpit nawigacyjny studio hello R dostępu](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Pulpit nawigacyjny studio hello R dostępu](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Niezależnie od zastosowanej metody hello hello logujesz się po raz pierwszy należy tooauthenticate dwa razy.  Na powitania pierwszego uwierzytelniania, zapewniają hello *nazwa użytkownika administratora klastra* i *hasło*. W drugim wierszu hello umożliwiające hello *nazwa użytkownika SSH* i *hasło*. Dziennik kolejne dodatki wymagać tylko hello *hasło SSH* i *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Połączenie z węzłem krawędzi serwera R toohello

Połączenie z węzłem krawędzi serwera tooR hello klastra usługi HDInsight przy użyciu protokołu SSH za pomocą polecenia hello:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Można znaleźć hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adresu w hello portalu Azure, wybierając klastra następnie **wszystkie ustawienia** -> **aplikacje** -> **użyciu polecenia RServer**. Zostaną wyświetlone informacje o punkcie końcowym SSH dla węzła krawędzi hello hello.
>
> ![Obraz powitania punkt końcowy SSH dla węzła krawędzi hello](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Jeśli użyto toosecure hasło konta użytkownika SSH, to zostanie wyświetlony monit o tooenter go. Jeśli używasz klucza publicznego, może być toouse hello `-i` toospecify parametru hello odpowiedniego klucza prywatnego. Na przykład:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Aby uzyskać więcej informacji, zobacz [połączyć tooHDInsight (Hadoop) przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

Po nawiązaniu połączenia przyjeździe monitu o podobnych następujące toohello:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Włączanie obsługi równoczesnych użytkowników

Można włączyć wiele równoczesnych użytkowników, dodając więcej użytkowników dla węzła krawędzi hello, na które hello społeczności programu RStudio uruchamia wersję.

Podczas tworzenia klastra usługi HDInsight musisz podać dwóch użytkowników: użytkownika HTTP i użytkownika SSH:

![Równoczesny użytkownik 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Nazwa użytkownika logowania klastra**: HTTP użytkownika do uwierzytelniania za pośrednictwem bramy HDInsight hello, która jest używana tooprotect hello HDInsight clusters utworzony. Ten użytkownik HTTP jest używane tooaccess hello interfejsu użytkownika narzędzia Ambari, interfejsie użytkownika YARN, jak również inne składniki interfejsu użytkownika.
- **Bezpiecznej powłoki (SSH) username**: SSH użytkownika tooaccess hello klastra za pośrednictwem bezpiecznej powłoki. Ten użytkownik jest użytkownikiem w hello systemu Linux dla wszystkich węzłów głównych hello węzłów procesu roboczego i węzły krawędzi. Aby można było korzystać tooaccess bezpiecznej powłoki dowolny z węzłów hello w zdalnym klastrze.

Witaj R Studio Server Community wersja programu używana w hello Microsoft R Server w klastrze usługi HDInsight typu akceptuje tylko Linux nazwę użytkownika i hasło jako mechanizm logowania. Przekazywanie tokenów nie jest obsługiwane. Tak, jeśli utworzono nowy klaster, a toouse tooaccess R Studio, należy toolog w dwa razy.

- Najpierw zalogować się przy użyciu poświadczeń użytkownika hello HTTP za pośrednictwem hello bramy usługi HDInsight: 

    ![Równoczesny użytkownik 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Następnie użyj toolog poświadczenia użytkownika SSH hello w tooRStudio:
  
    ![Równoczesny użytkownik 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Aktualnie podczas aprowizowania klastra usługi HDInsight można utworzyć tylko jedno konto użytkownika SSH. Dlatego tooenable wielu użytkowników tooaccess Microsoft R Server w usłudze HDInsight clusters, potrzebujemy toocreate dodatkowym użytkownikom w hello systemu Linux.

Ponieważ programu RStudio społeczności serwera jest uruchomiona w węźle krawędzi hello klastra, istnieje kilka kroków w tym miejscu:

1. Użyj toolog użytkownika SSH hello utworzone w węźle krawędzi toohello
2. Dodaj użytkowników systemu Linux w węźle krawędzi
3. Wersja ciągu identyfikacyjnego programu RStudio za pomocą hello utworzonych przez użytkownika

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Krok 1: Stosowanie toolog użytkownika SSH hello utworzone w węźle krawędzi toohello

Pobranie dowolnego narzędzia SSH (takiego jak Putty) i użycie hello istniejących SSH użytkownika toolog w. Następnie wykonaj hello instrukcje podane w [połączyć tooHDInsight (Hadoop) przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello węzła krawędzi. jest Hello adres węzła krawędzi serwera R w klastrze usługi HDInsight: *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Krok 2. Dodawanie użytkowników systemu Linux w węźle krawędzi

tooadd węzła krawędzi toohello użytkownika, wykonaj polecenia hello:

    sudo useradd yournewusername -m
    sudo passwd yourusername

Powinny pojawić się hello następujących elementów zwróconych: 

![Równoczesny użytkownik 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

Po wyświetleniu monitu o "bieżące hasło protokołu Kerberos:", wystarczy nacisnąć klawisz **Enter** tooignore go. Witaj `-m` opcji `useradd` polecenie wskazuje, że hello system utworzy folder macierzysty użytkownika hello, co jest wymagane dla wersji społeczności programu RStudio.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Krok 3: Użyj programu RStudio społeczności wersji z hello utworzonych przez użytkownika

Użyj hello toolog utworzonych przez użytkownika w tooRStudio:

![Równoczesny użytkownik 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Powiadomienia programu RStudio wskazuje, że używasz hello nowego użytkownika (tutaj, na przykład *sshuser6*) toolog hello klastra: 

![Równoczesny użytkownik 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

Możesz także zalogować się przy użyciu poświadczeń oryginalnego hello (domyślnie jest *sshuser*) jednocześnie z innego okna przeglądarki.

Zadania można przesyłać za pomocą funkcji programu ScaleR. Oto przykład toorun polecenia używane hello zadania:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Zwróć uwagę, czy zadania hello przekazane w różnych nazw użytkowników w interfejsie użytkownika YARN:

![Równoczesny użytkownik 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Uwaga również tego hello nowo dodanych użytkowników nie mają uprawnień do katalogu głównego w systemie Linux, ale one mieć hello tego samego dostępu do plików hello tooall hello systemu plików HDFS i WASB magazynu zdalnego.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Za pomocą konsoli hello R

1. Hello sesji SSH używając hello następujące polecenia toostart hello R konsoli:  

        R

2. Powinny pojawić się dane wyjściowe podobne toohello poniżej:
    
    Wersja 3.2.2 (2015-08-14)--"Fire bezpieczeństwa" Copyright (C) 2015 R hello R Foundation dla platformy przetwarzania danych statystycznych: x86_64-komputer linux-gnu (64-bitowe)

    Bezpłatne oprogramowanie R jest dostarczane BEZ ŻADNEJ GWARANCJI.
    Jesteś tooredistribute powitalnej określonych warunkach.
    Wpisz „license()” lub „licence()”, aby uzyskać szczegółowe informacje o dystrybucji.

    Oprogramowanie obsługuje język naturalny, ale z angielskimi ustawieniami regionalnymi.

    R jest projektem zbiorowym, zrzeszającym wielu uczestników.
    Wpisz "contributors()" Aby uzyskać więcej informacji oraz "citation()" w sposób toocite R lub R pakietów w publikacji.

    Typ "demo()" dla niektórych pokazów, "help()", aby uzyskać pomoc online lub "help.start()" dla toohelp Interfejs przeglądarki HTML.
    Wpisz "q()" tooquit R.

    Oprogramowanie Microsoft R Server w wersji 8.0: rozszerzona dystrybucja pakietów R firmy Microsoft. Copyright (C) 2016 Microsoft Corporation

    Aby uzyskać informacje o wersji, wpisz „readme()”.
    >

3. Z hello `>` monitu, można wprowadzić kod R. Serwer R obejmuje pakiety, które pozwalają tooeasily interakcji z Hadoop i uruchom rozproszone obliczenia. Na przykład można użyć następującego polecenia tooview hello głównym hello domyślnego systemu plików dla klastra usługi HDInsight hello hello:

    rxHadoopListFiles("/")

4. Umożliwia również hello WASB styl adresowania.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Używanie oprogramowania R Server w usłudze HDI ze zdalnego wystąpienia oprogramowania Microsoft R Server lub programu Microsoft R Client

Jest możliwe tooset się dostępu toohello HDI Hadoop Spark obliczeń kontekstu ze zdalnego wystąpienia programu Microsoft R Server lub uruchomione na pulpicie lub laptop klienta R firmy Microsoft. Zobacz **przy użyciu Microsoft R Server jako klienta usługi Hadoop** podsekcji w hello [tworzenie kontekst obliczeniowe dla Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo tak, konieczne jest hello toospecify następujące opcje, definiując kontekstu obliczeń RxSpark hello na laptopie: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches i sshProfileScript. Na przykład:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Używanie kontekstu obliczeniowego

Kontekst obliczeń umożliwia toocontrol obliczeń jest wykonywana lokalnie na węzeł brzegowy hello lub rozproszone na powitania węzłach w klastrze usługi HDInsight hello.

1. Z serwera programu RStudio lub konsoli hello R (w sesji SSH) Użyj następującego kodu tooload przykładowe dane do magazynu domyślnego powitania dla usługi HDInsight hello:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Następnie umożliwia tworzenie niektóre informacje o danych i zdefiniowanie dwóch źródeł danych, tak aby firma Microsoft może współpracować z hello danych.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Teraz uruchom Regresja logistyczna nad danymi hello przy użyciu kontekstu obliczeń lokalne powitania.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Powinny pojawić się dane wyjściowe, która kończy się toohello podobne wiersze po:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Następnie uruchom teraz hello tego samego Regresja logistyczna przy użyciu kontekstu Spark hello. kontekst Spark Hello dystrybuuje hello przetwarzania za pośrednictwem wszystkich węzłów procesu roboczego hello hello klastra usługi HDInsight.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > Umożliwia także MapReduce toodistribute obliczeń na węzłach klastra. Aby uzyskać więcej informacji na temat kontekstu obliczeniowego, zobacz [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight).


## <a name="distribute-r-code-toomultiple-nodes"></a>Dystrybuuj węzłów toomultiple kodu języka R

Z serwerem R, można łatwo zająć istniejącego kodu języka R i uruchom go na wielu węzłach w klastrze hello przy użyciu `rxExec`. Funkcja ta jest przydatna podczas czyszczenia parametrów lub przeprowadzania symulacji. Witaj następujący kod jest przykładem toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Jeśli nadal używasz hello Spark lub kontekstu MapReduce, to polecenie zwraca wartość nodename hello węzłów procesu roboczego hello kodu hello `(Sys.info()["nodename"])` jest uruchamiane na. Na przykład w klastrze czterema węzłami, prawdopodobnie tooreceive dane wyjściowe podobne toohello następujące czynności:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Dostęp do danych w usługach Hive i Parquet

Funkcja dostępna w R Server 9.1 umożliwia toodata bezpośredni dostęp do gałęzi i Parquet do użycia przez funkcje ScaleR w kontekście obliczeń Spark hello. Te funkcje są dostępne nowe ScaleR źródła funkcji danych o nazwie RxHiveData i RxParquetData współpracujących przy użyciu programu Spark SQL tooload dane bezpośrednio do DataFrame Spark, do analizy przez ScaleR.  

Witaj następującego kodu zawiera niektóre przykładowy kod przy użyciu nowych funkcji hello:

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Aby uzyskać dodatkowe informacje dotyczące użycia tych nowych funkcji, zobacz Pomoc online hello R Server przy użyciu hello `?RxHivedata` i `?RxParquetData` poleceń.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Zainstaluj dodatkowe pakiety języka R w węźle krawędzi hello

Jeśli chcesz, dodatkowe pakiety języka R tooinstall na węzeł brzegowy hello, możesz użyć `install.packages()` bezpośrednio z poziomu hello R konsoli po połączonych toohello krawędzi węzła za pośrednictwem protokołu SSH. Jednak pakiety języka R tooinstall na powitania węzłów procesu roboczego hello klastra, należy należy użyć akcji skryptu.

Akcje skryptu to skrypty Bash, które są używane toomake konfiguracji zmiany toohello HDInsight klastra lub tooinstall dodatkowego oprogramowania, np. dodatkowe pakiety języka R. tooinstall dodatkowe pakiety przy użyciu akcji skryptu, użyj hello następujące kroki:

> [!IMPORTANT]
> Za pomocą akcji skryptu tooinstall dodatkowe pakiety języka R można używać tylko po utworzeniu klastra hello. Nie należy używać tej procedury podczas tworzenia klastra, ponieważ skrypt hello korzysta z tego serwera R całkowicie zainstalowana i skonfigurowana.
>
>

1. Z hello [portalu Azure](https://portal.azure.com), wybierz serwer R w klastrze usługi HDInsight.

2. Z hello **ustawienia** bloku, wybierz opcję **akcji skryptu** , a następnie **przesłać nowe** toosubmit nowa akcja skryptu.

   ![Obraz bloku akcji skryptu](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. Z hello **przesłać akcji skryptu** bloku, podaj hello następujących informacji:

   * **Nazwa**: przyjazną nazwę tego skryptu tooidentify

   * **Identyfikator URI skryptu powłoki systemowej**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Główny**: to pole powinno być **niezaznaczone**

   * **Proces roboczy**: to pole powinno być **zaznaczone**

   * **Węzły krawędzi**: to pole powinno być **niezaznaczone**

   * **Dozorca**: to pole powinno być **niezaznaczone**

   * **Parametry**: toobe zainstalowanych pakietów hello R. Na przykład: `bitops stringr arules`

   * **Utrwal ten skrypt...**: to pole powinno być **zaznaczone**  

   > [!NOTE]
   > 1. Domyślnie wszystkie pakiety języka R są zainstalowane z migawki spójne z wersją powitania serwera R, która została zainstalowana repozytorium Microsoft MRAN hello. Jeśli chcesz tooinstall nowsze wersje pakietów, oznacza to, że niektóre ryzyka niezgodności. Jednak tego rodzaju instalacji jest możliwe określenie `useCRAN` jako hello pierwszego elementu obiektu pakietów hello listy, na przykład `useCRAN bitops, stringr, arules`.  
   > 2. Niektóre pakiety R wymagają dodatkowych bibliotek systemu Linux. Dla wygody firma Microsoft wstępnie zainstalować zależności hello wymagane przez hello pierwszych 100 najpopularniejszych R pakietów. Jednak jeśli hello R pakiety, które będą instalowane wymagają bibliotek poza te następnie należy pobrać hello skryptu podstawowy używany w tym miejscu i dodać biblioteki systemu hello tooinstall czynności. Należy najpierw, a następnie przekazywania hello zmodyfikować skrypt tooa publicznego kontenera w magazynie Azure obiektów blob i korzystanie z pakietów hello tooinstall skryptu hello zmodyfikowane.
   >    Aby uzyskać informacje na temat tworzenia akcji skryptu, zobacz [Script Action development](hdinsight-hadoop-script-actions-linux.md) (Tworzenie akcji skryptu).  
   >
   >

   ![Dodawanie akcji skryptu](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Wybierz **Utwórz** toorun hello skryptu. Po ukończeniu działania skryptu hello pakietów hello R są dostępne na wszystkich węzłów procesu roboczego.


## <a name="using-microsoft-r-server-operationalization"></a>Używanie funkcji opernacjonalizacji oprogramowania Microsoft R Server

Po zakończeniu Twojej modelowania danych, aby operacjonalizować hello modelu toomake prognoz. tooconfigure dla operationalization Microsoft R Server wykonaj hello następujące kroki:

Najpierw ssh do węzła krawędzi hello. Na przykład: 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Po użyciu ssh, zmień katalog dla wersji odpowiednich hello i sudo hello dotnet dll: 

- W przypadku oprogramowania Microsoft R Server 9.1:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- W przypadku oprogramowania Microsoft R Server 9.0:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

operationalization Microsoft R Server tooconfigure z konfiguracją jednego pola hello następujące:

1. Wybierz pozycję „Configure R Server for Operationalization” (Konfiguruj oprogramowanie R Server pod kątem operacjonalizacji)
2. Wybierz pozycję „A. One-box (web + compute nodes)” (Jedna maszyna — sieć Web i węzły obliczeniowe)
3. Wprowadź hasło dla hello **admin** użytkownika

![opernacjonalizacja przy użyciu jednej maszyny](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

Opcjonalnie możesz wykonać kontrolę diagnostyczną, uruchamiając test diagnostyczny w sposób pokazany poniżej:

1. Wybierz pozycję „6. Run diagnostic tests” (Uruchom testy diagnostyczne)
2. Wybierz pozycję „A. Test configuration” (Testuj konfigurację)
3. Wpisz ciąg Username = “admin” i hasło określone w poprzednim kroku konfiguracji
4. Potwierdź wynik: Overall Health = pass (Ogólna kondycja — dobra)
5. Administrator narzędzie hello zakończenia
6. Zamknij połączenie SSH

![Diagnostyka opernacjonalizacji](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Duże opóźnienia podczas używania usługi internetowej na platformie Spark**
>
>Jeśli wystąpią duże opóźnienia podczas próby tooconsume usługi sieci web utworzone za pomocą funkcji mrsdeploy w kontekście obliczeń Spark, może być konieczne tooadd niektórych Brak folderów. Witaj aplikacji Spark należy tooa użytkownika o nazwie "*rserve2*" zawsze, gdy jest wywoływana z usługi sieci web przy użyciu funkcji mrsdeploy. toowork uniknąć tego problemu:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


Na tym etapie hello Konfiguracja Operationalization jest pełny. Teraz można używać mrsdeploy"hello" pakiet w Twojej toohello tooconnect RClient Operationalization węzła krawędzi i rozpocząć korzystanie z jej funkcje, takie jak [zdalne wykonywanie kodu](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) i [usług sieci web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). W zależności od tego, czy klastra jest skonfigurowana w sieci wirtualnej lub nie może być konieczne tooset zapasowej portu do przodu tunelowania przez logowania SSH. Witaj poniższe sekcje zawierają opis sposobu tooset się ten tunel.

### <a name="rserver-cluster-on-virtual-network"></a>Klaster oprogramowania RServer w sieci wirtualnej

Upewnij się, że można zezwolić na ruch przez port 12800 toohello węzłem krawędzi. Dzięki temu funkcja hello krawędzi węzła tooconnect toohello Operationalization.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Jeśli hello `remoteLogin()` nie może połączyć się z węzłem krawędzi toohello, ale można węzła krawędzi toohello SSH, a następnie należy tooverify czy hello reguły tooallow ruch na porcie 12800 został ustawiony prawidłowo lub nie. Jeśli będziesz kontynuować tooface hello problem, możesz można obejść, poprzez ustawienie portu do przodu tunelowania za pośrednictwem protokołu SSH. Aby uzyskać instrukcje Zobacz hello następujących sekcji.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>Klaster oprogramowania RServer w sieci niewirtualnej

Jeśli klaster nie jest skonfigurowany w sieci wirtualnej lub występują problemy z korzystaniem z sieci wirtualnej, możesz użyć tunelowania przekierowania portów za pomocą protokołu SSH:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

W programie Putty także możesz je skonfigurować.

![połączenie ssh w programie putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Po aktywnej sesji SSH hello z tego komputera, portu 12800 przekazywane są węzłem krawędzi toohello portu 12800 za pośrednictwem sesji SSH. Upewnij się, że w metodzie `remoteLogin()` użyto adresu `127.0.0.1:12800`. Loguje operationalization węzłem krawędzi toohello za pomocą przekierowania portów.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Jak tooscale Microsoft R Server Operationalization obliczeniowe węzłów w usłudze HDInsight węzłów procesu roboczego

### <a name="decommission-hello-worker-nodes"></a>Likwidowanie hello węzłów procesu roboczego

Oprogramowanie Microsoft R Server nie jest aktualnie zarządzane za pomocą usługi Yarn. Jeśli hello węzłów procesu roboczego nie są wycofany z eksploatacji, hello Yarn Menedżera zasobów nie będzie działać zgodnie z oczekiwaniami, ponieważ nie będą świadomi hello zasobów zostanie pobrana przez powitania serwera. W kolejności tooavoid tej sytuacji, firma Microsoft zaleca likwidowania węzłów procesu roboczego hello przed skalowanie węzłów obliczeniowych hello.

Kroki toodecommissioning węzłów procesu roboczego:

* Zaloguj się w konsoli narzędzia Ambari tooHDI klastra i kliknij na karcie "hostów"
* Wybierz węzłów procesu roboczego (toobe zlikwidowana), kliknij pozycję "Akcje" > "Wybrane hosty" > "Hostów" > kliknij "Włącz ON konserwacji tryb". Na przykład w następujących obraz powitania Wybraliśmy toodecommission wn3 i wn4.  

   ![likwidowanie węzłów procesu roboczego](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Wybierz pozycję **Actions** > **Selected Hosts** > **DataNodes** (Akcje > Wybrane hosty > Węzły danych) i kliknij pozycję **Decommission** (Likwiduj)
* Wybierz pozycję **Actions** > **Selected Hosts** > **NodeManagers** (Akcje > Wybrane hosty > Menedżerowie węzła) i kliknij pozycję **Decommission** (Likwiduj)
* Wybierz pozycję **Actions** > **Selected Hosts** > **DataNodes** (Akcje > Wybrane hosty > Węzły danych) i kliknij pozycję **Stop** (Zatrzymaj)
* Wybierz pozycję **Actions** > **Selected Hosts** > **NodeManagers** (Akcje > Wybrane hosty > Menedżerowie węzła) i kliknij pozycję **Stop** (Zatrzymaj)
* Wybierz pozycję **Actions** > **Selected Hosts** > **Hosts** (Akcje > Wybrane hosty > Hosty) i kliknij pozycję **Stop All Components** (Zatrzymaj wszystkie składniki)
* Usuń zaznaczenie hello węzłów procesu roboczego, a następnie wybierz hello węzłów głównych
* Wybierz pozycję **Actions** > **Selected Hosts** > **Hosts** > **Restart All Components** (Akcje > Wybrane hosty > Hosty > Uruchom ponownie wszystkie składniki)

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Konfigurowanie węzłów obliczeniowych na wszystkich zlikwidowanych węzłach procesu roboczego

1. Za pomocą protokołu SSH połącz się z każdym zlikwidowanym węzłem procesu roboczego.
2. Uruchom narzędzie administracyjne za pomocą polecenia `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Wprowadź "1" tooselect opcję "Konfiguruj dla Operationalization serwera R".
4. Wybierz opcję "c" tooselect "C. Compute node” (Węzeł obliczeniowy). Spowoduje to skonfigurowanie węzeł obliczeniowy hello na powitania węzła procesu roboczego.
5. Administrator narzędzie hello zakończenia.

### <a name="add-compute-nodes-details-on-web-node"></a>Dodawanie szczegółów węzłów obliczeniowych na węźle sieci Web

Po skonfigurowaniu wszystkich węzłów procesu roboczego wycofany z eksploatacji toorun węzła obliczeniowego, wróć na węzeł brzegowy hello i dodać węzłów procesu roboczego wycofany z eksploatacji adresów IP w konfiguracji węzła hello R serwera sieci web:

* SSH do węzła krawędzi hello.
* Uruchom polecenie `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
* Wyszukaj sekcję "URI" hello i Dodaj IP węzła procesu roboczego i Szczegóły portu.

    ![wiersz polecenia likwidowania węzłów procesu roboczego](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Następne kroki

Teraz należy zrozumieć, jak toocreate nowego klastra usługi HDInsight, który obejmuje hello R Server i hello posługiwać się hello konsoli R w sesji SSH. Witaj poniższych tematach opisano inne sposoby zarządzania i Praca z serwerem R w usłudze HDInsight:

* [Dodaj serwer programu RStudio tooHDInsight (Jeśli nie zainstalowano podczas tworzenia klastra)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)
* [Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)
