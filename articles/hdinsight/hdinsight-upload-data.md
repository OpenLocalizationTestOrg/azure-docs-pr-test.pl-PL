---
title: "aaaUpload danych dotyczących zadań Hadoop w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupload i dostępu do danych dotyczących zadań Hadoop w usłudze HDInsight przy użyciu hello Azure CLI, Eksploratora usługi Storage platformy Azure, programu Azure PowerShell, wiersza polecenia platformy Hadoop hello lub Sqoop."
keywords: "etl hadoop, pobieranie danych do platformy hadoop, hadoop ładowanie danych"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Przekazywanie danych dla zadań Hadoop w usłudze HDInsight
Usługa Azure HDInsight udostępnia kompletne rozproszonego systemu plików usługi Hadoop (HDFS) w porównaniu z magazynu obiektów Blob platformy Azure. Zaprojektowano go jako tooprovide rozszerzenia systemu plików HDFS bezproblemowej wystąpić toocustomers. Umożliwia on hello pełny zestaw składników w toooperate ekosystemu Hadoop hello bezpośrednio na powitania danych, którymi zarządza. Azure Blob storage i system plików HDFS są systemy różnych plików, które są zoptymalizowane pod kątem przechowywania danych i obliczenia na tych danych. Aby uzyskać informacje dotyczące korzyści hello przy użyciu magazynu obiektów Blob platformy Azure, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].

**Wymagania wstępne**

Należy uwzględnić następujące wymagania przed rozpoczęciem powitalne:

* Klaster Azure HDInsight. Aby uzyskać instrukcje, zobacz [Rozpoczynanie pracy z usługą Azure HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].

## <a name="why-blob-storage"></a>Dlaczego magazynu obiektów blob?
Usługa Azure HDInsight klastry są zwykle wdrażane toorun zadań MapReduce, a klastry hello są usuwane po zakończeniu tych zadań. Utrzymywanie hello danych w klastrach systemu plików HDFS hello po zakończeniu obliczenia byłoby toostore sposób kosztowne tych danych. Magazyn obiektów Blob Azure jest wysokiej dostępności, wysokiej skalowalności i wysokiej wydajności, opcja niskich kosztów i możliwe do udostępnienia magazynowania danych, które jest toobe przetworzona za pomocą usługi HDInsight. Zapisywanie danych w obiekcie blob umożliwia hello klastrów usługi HDInsight, które są używane do obliczeń toobe bezpiecznie wydana bez utraty danych.

### <a name="directories"></a>Katalogi
Kontenery magazynu obiektów Blob platformy Azure przechowują dane jako pary klucz wartość, a istnieje bez hierarchii katalogów. Jednak Witaj "/" znak może być używana w toomake nazwa klucza hello wydaje się tak, jakby plik był przechowywany w ramach struktury katalogów. HDInsight widzi je tak, jakby są rzeczywiste katalogów.

Na przykład klucz obiektu blob może mieć postać *input/log1.txt*. Nie rzeczywiste katalogu "wejściowym" istnieje, ale powodu obecności toohello hello znak "/" w nazwie klucza hello, ma wygląd hello ścieżki do pliku.

W związku z tym Jeśli używasz narzędzia Azure Explorer mogą pojawić się niektóre pliki 0 bajtów. Te pliki służą do dwóch celów:

* Jeśli występują puste foldery, oznacz istnienia hello hello folderu. Magazyn obiektów Blob Azure jest wystarczająco inteligentne tooknow, że jeśli obiektu blob o nazwie foo/pasek istnieje, jest folder o nazwie **foo**. Ale hello tylko toosignify sposób pusty folder o nazwie **foo** jest posiadanie tego pliku specjalne 0 bajtów.
* Blokady są specjalne metadane, które są wymagane przez hello Hadoop systemu plików, szczególnie hello uprawnienia i właścicieli hello folderów.

## <a name="command-line-utilities"></a>Narzędzia wiersza polecenia
Firma Microsoft udostępnia hello następujące narzędzia toowork z magazynu obiektów Blob platformy Azure:

| Narzędzie | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Interfejs wiersza polecenia platformy Azure][azurecli] |✔ |✔ |✔ |
| [Program Azure PowerShell][azure-powershell] | | |✔ |
| [Narzędzie AzCopy][azure-azcopy] | | |✔ |
| [Polecenie Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Gdy hello wiersza polecenia platformy Azure, programu Azure PowerShell i narzędzia AzCopy można wszystkie można używać z zewnętrznej platformy Azure, hello Hadoop polecenia jest dostępna tylko na powitania klastra usługi HDInsight i zezwala na tylko podczas ładowania danych z hello lokalnego systemu plików do magazynu obiektów Blob platformy Azure.
>
>

### <a id="xplatcli"></a>Interfejs wiersza polecenia platformy Azure
Hello wiersza polecenia platformy Azure to narzędzie i platform, które pozwala toomanage Azure usługi. Użyj powitania po magazynu obiektów Blob tooAzure danych tooupload kroki:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Instalowanie i konfigurowanie hello Azure CLI for Mac, Linux i Windows](../cli-install-nodejs.md).
2. Otwórz wiersz polecenia, bash lub innego powłoki i użyj powitania po tooyour tooauthenticate subskrypcji platformy Azure.

        azure login

    Po wyświetleniu monitu wprowadź hello nazwę użytkownika i hasło dla Twojej subskrypcji.
3. Wprowadź hello następujących kont magazynu hello toolist polecenia dla Twojej subskrypcji:

        azure storage account list
4. Wybierz konto magazynu hello zawierający hello obiektów blob, który ma toowork z, a następnie użyj powitania po klucz hello tooretrieve polecenia dla tego konta:

        azure storage account keys list <storage-account-name>

    Powinny zostać zwrócone **głównej** i **dodatkowej** kluczy. Kopiuj hello **głównej** wartość klucza, ponieważ będzie on używany w następnych krokach hello.
5. Użyj następującego polecenia tooretrieve listę kontenerów obiektów blob w ramach konta magazynu hello hello:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Użyj następującego polecenia tooupload hello i pobierania plików toohello blob:

   * tooupload pliku:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload pliku:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Jeśli będziesz zawsze pracować z hello same konta magazynu, możesz ustawić hello następujące zmienne środowiskowe zamiast określania hello konta i klucz dla każdego polecenia:
>
> * **AZURE\_MAGAZYNU\_konta**: Nazwa konta magazynu hello
> * **AZURE\_MAGAZYNU\_dostępu\_klucza**: klucz konta magazynu hello
>
>

### <a id="powershell"></a>Program Azure PowerShell
Program Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania obciążeń na platformie Azure. Aby uzyskać informacje o konfigurowaniu toorun Twojego stacji roboczej programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload tooAzure lokalnego pliku magazynu obiektów Blob**

1. Otwórz hello Azure PowerShell konsoli zgodnie z instrukcją w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
2. Ustaw wartości hello hello pierwsze pięć zmiennych w hello następującego skryptu:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Wklej hello do toorun konsoli programu Azure PowerShell hello go toocopy hello plik skryptu.

Na przykład toowork utworzonych skryptów programu PowerShell z usługą HDInsight, zobacz [narzędzi HDInsight tools](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>Narzędzie AzCopy
Narzędzie AzCopy to narzędzie wiersza polecenia, które są zaprojektowane toosimplify hello zadanie transferu danych do i z konta usługi Azure Storage. Można używać jej jako autonomicznego narzędzia lub włączyć to narzędzie w istniejącej aplikacji. [Pobierz narzędzia AzCopy][azure-azcopy-download].

Składnia narzędzia AzCopy Hello jest:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Aby uzyskać więcej informacji, zobacz [AzCopy - przekazywania/pobieranie plików dla obiektów blob Azure][azure-azcopy].

### <a id="commandline"></a>Wiersz polecenia usługi Hadoop
Wiersz polecenia Hadoop Hello jest przydatna do przechowywania danych do magazynu obiektów blob, gdy dane hello jest już obecny na powitania węzła głównego klastra.

W kolejności toouse hello polecenia Hadoop należy połączyć headnode toohello przy użyciu jednej z następujących metod hello:

* **HDInsight opartych na systemie Windows**: [łączyć się przy użyciu pulpitu zdalnego](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight opartych na systemie Linux**: połączenie przy użyciu protokołu SSH ([hello polecenia SSH](hdinsight-hadoop-linux-use-ssh-unix.md) lub [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Po nawiązaniu połączenia można użyć hello następującej składni tooupload toostorage pliku.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Na przykład: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Ponieważ hello domyślnego systemu plików dla usługi HDInsight znajduje się w magazynie obiektów Blob Azure, /example/data.txt jest rzeczywiście w magazynie obiektów Blob Azure. Znajdują się w pliku toohello jako:

    wasb:///example/data/data.txt

lub

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Aby uzyskać listę innych Hadoop polecenia pracy z plikami, zobacz [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> W przypadku klastrów HBase hello domyślny rozmiar bloku używany podczas zapisywania danych 256KB. Gdy nie ma problemów podczas korzystania z interfejsów API HBase lub interfejsów API REST, przy użyciu hello `hadoop` lub `hdfs dfs` większych niż ~ 12 GB danych toowrite polecenia powoduje błąd. Zobacz hello [wyjątek magazynu do zapisu dla obiektu blob](#storageexception) sekcji poniżej, aby uzyskać więcej informacji.
>
>

## <a name="graphical-clients"></a>Klientach graficznego
Istnieje kilka aplikacji, które zapewniają interfejs graficzny służący do pracy z usługą Azure Storage. Witaj poniżej znajduje się lista niektóre z tych aplikacji:

| Klient | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio Tools dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure Storage Explorer](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Chmura magazynu Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Eksplorator systemu Azure](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio Tools dla usługi HDInsight
Aby uzyskać więcej informacji, zobacz [hello Nawigacja połączonych zasobów](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Eksplorator usługi Storage platformy Azure
*Eksplorator usługi Storage Azure* stanowi przydatne narzędzie sprawdzania i zmienianie hello danych w obiektach blob. To narzędzie wolnego typu open source, który można pobrać z [http://storageexplorer.com/](http://storageexplorer.com/). Kod źródłowy Hello jest dostępna z tego łącza, a także.

Przed użyciem narzędzia hello, musisz znać Azure klucz konta magazynu nazwy i konta. Aby uzyskać instrukcje dotyczące pobierania tych informacji, zobacz hello "jak: widoku, kopiowania i regenerate magazynu klucze dostępu" sekcji [tworzenia, zarządzania i usuwania konta magazynu][azure-create-storage-account].

1. Uruchom Eksploratora usługi Storage platformy Azure. Jeśli po raz pierwszy hello uruchomieniu hello Eksploratora usługi Storage, zostanie wyświetlony monit dla hello **nazwa konta miej_sca VM** i **klucz konta magazynu**. Po uruchomieniu go przed Użyj hello **Dodaj** przycisk tooadd nazwę nowego konta magazynu i klucza.

    Wprowadź hello nazwy i klucza dla konta magazynu hello korzystali z klastrem usługi HDInsight, a następnie wybierz opcję **Otwórz z & APISZ**.

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. Na liście hello lewej toohello kontenery interfejsu hello kliknij nazwę hello hello kontenera, który jest skojarzony z klastrem usługi HDInsight. Domyślnie to jest nazwa hello hello klastra usługi HDInsight, ale mogą być inne, jeśli podczas tworzenia klastra hello wprowadzone określonej nazwy.
3. Z paska narzędzi hello wybierz ikonę przekazywania hello.

    ![Pasek narzędzi z ikoną przekazywania wyróżnione](./media/hdinsight-upload-data/toolbar.png)
4. Określ tooupload pliku, a następnie kliknij przycisk **Otwórz**. Po wyświetleniu monitu wybierz **przekazać** tooupload hello pliku toohello głównym hello kontenera magazynu. Jeśli chcesz tooupload hello pliku tooa określonej ścieżki, wprowadź ścieżkę hello w hello **docelowego** pola, a następnie wybierz **przekazać**.

    ![Okno dialogowe przekazywania pliku](./media/hdinsight-upload-data/fileupload.png)

    Po zakończeniu hello plików podczas przekazywania, można go z zadań w klastrze usługi HDInsight hello.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Magazyn obiektów Blob Azure instalacji jako dysk lokalny
Zobacz [magazyn obiektów Blob Azure instalacji jako dysk lokalny](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Usługi
### <a name="azure-data-factory"></a>Azure Data Factory
Hello usługi fabryka danych Azure jest w pełni zarządzaną usługę służącą do tworzenia magazynu, przetwarzanie danych i danych usługi przenoszenia danych usługi w potokach produkcji prostsze, skalowalne i niezawodne danych.

Fabryka danych Azure mogą być używane toomove dane do magazynu obiektów Blob platformy Azure lub toocreate potokach danych, które bezpośrednio takich jak używać funkcji usługi HDInsight Hive i wieprzowych.

Aby uzyskać więcej informacji, zobacz hello [dokumentacji fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop to narzędzie przeznaczone tootransfer danych pomiędzy platformą Hadoop a relacyjnymi bazami danych. Umożliwia tooimport danych z systemu zarządzania relacyjnymi bazami danych (RDBMS), takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed hello (HDFS), przekształcania danych hello w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować hello danych do RDBMS.

Aby uzyskać więcej informacji, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>Programowanie zestawów SDK
Magazyn obiektów Blob Azure można również uzyskać dostęp przy użyciu zestawu SDK platformy Azure z hello następujące języki programowania:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Aby uzyskać więcej informacji na temat instalowania hello Azure SDK, zobacz [Azure pliki do pobrania.](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a id="storageexception"></a>Wyjątek magazynu do zapisu dla obiektu blob
**Objawy**: przy użyciu hello `hadoop` lub `hdfs dfs` polecenia toowrite pliki, które są ~ 12 GB lub większy na klaster HBase, można napotkać hello następujący błąd:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Przyczyna**: bazy danych HBase w usłudze HDInsight clusters domyślny rozmiar bloku tooa 256 KB, podczas zapisywania tooAzure magazynu. Gdy działa to w przypadku interfejsu API REST lub interfejsów API HBase, spowoduje błąd przy użyciu hello `hadoop` lub `hdfs dfs` narzędzi wiersza polecenia.

**Rozdzielczość**: Użyj `fs.azure.write.request.size` toospecify większy rozmiar bloku. Należy na podstawie użycia za pomocą hello `-D` parametru. Witaj poniżej przedstawiono przykład użycia tego parametru z hello `hadoop` polecenia:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Można również zwiększyć wartość hello `fs.azure.write.request.size` globalnie, za pomocą narzędzia Ambari. Witaj czynności do wykonania może być używana wartość hello toochange w hello Interfejsu sieci Web Ambari:

1. W przeglądarce Przejdź toohello Interfejsu sieci Web Ambari dla klastra. Jest to https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest hello nazwą klastra.

    Po wyświetleniu monitu wprowadź nazwę administratora hello i hasło dla hello klastra.
2. Hello po lewej stronie ekranu hello, zaznacz **HDFS**, a następnie wybierz hello **Configs** kartę.
3. W hello **filtru...**  wprowadź `fs.azure.write.request.size`. Spowoduje to wyświetlenie hello pola i bieżąca wartość w środku hello hello strony.
4. Zmień wartość hello z 262144 (256KB) toohello nową wartość. Na przykład 4194304 (4MB).

![Obraz zmiany wartości hello za pośrednictwem interfejsu użytkownika sieci Web Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrów usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari hello](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Następne kroki
Zapoznaniu się jak tooget danych do usługi HDInsight, przeczytaj hello następujące artykuły toolearn jak tooperform analizy:

* [Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]
* [Przesyłanie zadań Hadoop programowo][hdinsight-submit-jobs]
* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
