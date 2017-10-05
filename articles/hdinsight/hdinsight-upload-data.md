---
title: "Przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przekazywanie i uzyskać dostęp do danych dotyczących zadań Hadoop w usłudze HDInsight przy użyciu wiersza polecenia platformy Azure, Eksploratora usługi Storage platformy Azure, programu Azure PowerShell, wiersz polecenia Hadoop lub Sqoop."
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Przekazywanie danych dla zadań Hadoop w usłudze HDInsight
Usługa Azure HDInsight udostępnia kompletne rozproszonego systemu plików usługi Hadoop (HDFS) w porównaniu z magazynu obiektów Blob platformy Azure. Zaprojektowano go jako rozszerzenie systemu plików HDFS aby zapewnić bezproblemową obsługę klientów. Umożliwia on pełny zestaw składników w ekosystemie Hadoop do działania bezpośrednio na danych, którymi zarządza. Azure Blob storage i system plików HDFS są systemy różnych plików, które są zoptymalizowane pod kątem przechowywania danych i obliczenia na tych danych. Aby uzyskać informacje o zaletach przy użyciu magazynu obiektów Blob platformy Azure, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].

**Wymagania wstępne**

Przed rozpoczęciem należy uwzględnić następujące wymagania:

* Klaster Azure HDInsight. Aby uzyskać instrukcje, zobacz [Rozpoczynanie pracy z usługą Azure HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].

## <a name="why-blob-storage"></a>Dlaczego magazynu obiektów blob?
Klastry HDInsight Azure zwykle są wdrażane do uruchomienia zadań MapReduce, a klastry są usuwane po zakończeniu tych zadań. Przechowywanie danych w systemie plików HDFS klastrów po zakończeniu obliczenia będzie kosztowna sposób przechowywania tych danych. Magazyn obiektów Blob Azure jest wysokiej dostępności, wysokiej skalowalności i wysokiej wydajności, opcja niskich kosztów i możliwe do udostępnienia magazynowania danych, które mają być przetwarzane przy użyciu usługi HDInsight. Zapisywanie danych w obiekcie blob umożliwia klastrów usługi HDInsight, które są używane do obliczeń bezpiecznie wydana bez utraty danych.

### <a name="directories"></a>Katalogi
Kontenery magazynu obiektów Blob platformy Azure przechowują dane jako pary klucz wartość, a istnieje bez hierarchii katalogów. Jednak znak "/" umożliwia wewnątrz nazwy klucza wydawać tak, jakby plik był przechowywany w ramach struktury katalogów. HDInsight widzi je tak, jakby są rzeczywiste katalogów.

Na przykład klucz obiektu blob może mieć postać *input/log1.txt*. Nie rzeczywiste katalogu "wejściowym" istnieje, ale z powodu obecności znaku "/" w nazwie klucza ma wygląd ścieżki do pliku.

W związku z tym Jeśli używasz narzędzia Azure Explorer mogą pojawić się niektóre pliki 0 bajtów. Te pliki służą do dwóch celów:

* Jeśli występują puste foldery, oznacz istnienia folderu. Magazyn obiektów Blob Azure jest inteligentne dowiedzieć się, że istnienie obiektu blob o nazwie foo/pasek istnieje folder o nazwie **foo**. Jedynym sposobem oznaczającego pusty folder o nazwie, ale **foo** jest posiadanie tego pliku specjalne 0 bajtów.
* Posiadają specjalne metadanych, które są wymagane przez system plików Hadoop, szczególnie uprawnienia i właścicieli dla folderów.

## <a name="command-line-utilities"></a>Narzędzia wiersza polecenia
Firma Microsoft udostępnia następujące narzędzia do pracy z magazynem obiektów Blob Azure:

| Narzędzie | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Interfejs wiersza polecenia platformy Azure][azurecli] |✔ |✔ |✔ |
| [Program Azure PowerShell][azure-powershell] | | |✔ |
| [Narzędzie AzCopy][azure-azcopy] | | |✔ |
| [Polecenie Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Gdy wiersza polecenia platformy Azure, programu Azure PowerShell i narzędzia AzCopy można wszystkie można używać z zewnętrznej platformy Azure, Hadoop polecenia jest dostępna tylko w klastrze usługi HDInsight i zezwala na tylko podczas ładowania danych z lokalnego systemu plików do magazynu obiektów Blob platformy Azure.
>
>

### <a id="xplatcli"></a>Interfejs wiersza polecenia platformy Azure
Interfejsu wiersza polecenia Azure to narzędzie i platform, które umożliwia zarządzanie usługami Azure. Aby przekazać dane do magazynu obiektów Blob platformy Azure, wykonaj następujące kroki:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure dla komputerów Mac, Linux i Windows](../cli-install-nodejs.md).
2. Otwórz wiersz polecenia, bash lub innego powłoki i służą do uwierzytelniania do subskrypcji platformy Azure.

        azure login

    Po wyświetleniu monitu wprowadź nazwę użytkownika i hasło dla Twojej subskrypcji.
3. Wprowadź następujące polecenie, aby wyświetlić listę kont magazynu dla Twojej subskrypcji:

        azure storage account list
4. Wybierz konto magazynu, które zawiera blob, które mają być używane, a następnie użyj następującego polecenia, aby pobrać klucz dla tego konta:

        azure storage account keys list <storage-account-name>

    Powinny zostać zwrócone **głównej** i **dodatkowej** kluczy. Kopiuj **głównej** wartość klucza, ponieważ będzie on używany w następnych krokach.
5. Aby pobrać listę kontenerów obiektów blob w ramach konta magazynu, użyj następującego polecenia:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Przekazywania i pobierania plików do obiektu blob, użyj następujących poleceń:

   * Aby przekazać plik:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * Aby pobrać plik:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Jeśli będziesz zawsze pracować z tego samego konta magazynu, można ustawić następujące zmienne środowiskowe zamiast określania konta i klucz dla każdego polecenia:
>
> * **AZURE\_MAGAZYNU\_konta**: Nazwa konta magazynu
> * **AZURE\_MAGAZYNU\_dostępu\_klucza**: klucz konta magazynu
>
>

### <a id="powershell"></a>Program Azure PowerShell
Program Azure PowerShell jest środowiskiem skryptów, które umożliwia kontrolowanie i automatyzowania wdrażania i zarządzania obciążeń na platformie Azure. Aby uzyskać informacji na temat konfigurowania stacji roboczej do uruchomienia programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**Aby przekazać plik lokalny do magazynu obiektów Blob platformy Azure**

1. Otwórz konsolę programu Azure PowerShell, zgodnie z instrukcją w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
2. Ustaw wartości zmiennych pierwsze pięć w poniższym skrypcie:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Wklej skryptu w konsoli programu Azure PowerShell, aby uruchomić ją można skopiować pliku.

Na przykład skrypty programu PowerShell utworzone do pracy z usługą HDInsight, zobacz [narzędzi HDInsight tools](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>Narzędzie AzCopy
Narzędzie AzCopy to narzędzie wiersza polecenia, które jest przeznaczona do upraszcza zadanie transferu danych do i z konta usługi Azure Storage. Można używać jej jako autonomicznego narzędzia lub włączyć to narzędzie w istniejącej aplikacji. [Pobierz narzędzia AzCopy][azure-azcopy-download].

Składnia narzędzia AzCopy jest następująca:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Aby uzyskać więcej informacji, zobacz [AzCopy - przekazywania/pobieranie plików dla obiektów blob Azure][azure-azcopy].

### <a id="commandline"></a>Wiersz polecenia usługi Hadoop
W wierszu polecenia Hadoop tylko przydaje się do przechowywania danych do magazynu obiektów blob, gdy danych jest już obecny na węzła głównego klastra.

Aby można było użyć polecenia Hadoop, musisz najpierw połączyć się headnode przy użyciu jednej z następujących metod:

* **HDInsight opartych na systemie Windows**: [łączyć się przy użyciu pulpitu zdalnego](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight opartych na systemie Linux**: połączenie przy użyciu protokołu SSH ([polecenia SSH](hdinsight-hadoop-linux-use-ssh-unix.md) lub [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Po nawiązaniu połączenia można użyć następującej składni do przekazania pliku do magazynu.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Na przykład: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Ponieważ jest domyślny system plików dla usługi HDInsight w magazynie obiektów Blob platformy Azure, /example/data.txt jest rzeczywiście w magazynie obiektów Blob Azure. Możesz także zapoznać się plik jako:

    wasb:///example/data/data.txt

lub

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Aby uzyskać listę innych Hadoop polecenia pracy z plikami, zobacz [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> Na klastrów HBase domyślnie bloku rozmiar używany podczas zapisywania danych to 256KB. Gdy nie ma problemów podczas korzystania z interfejsów API HBase lub interfejsów API REST, za pomocą `hadoop` lub `hdfs dfs` polecenia do zapisania danych większych niż ~ 12 GB powoduje wystąpienie błędu. Zobacz [wyjątek magazynu do zapisu dla obiektu blob](#storageexception) sekcji poniżej, aby uzyskać więcej informacji.
>
>

## <a name="graphical-clients"></a>Klientach graficznego
Istnieje kilka aplikacji, które zapewniają interfejs graficzny służący do pracy z usługą Azure Storage. Poniżej przedstawiono listę niektóre z tych aplikacji:

| Klient | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio Tools dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure Storage Explorer](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Chmura magazynu Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Eksplorator systemu Azure](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio Tools dla usługi HDInsight
Aby uzyskać więcej informacji, zobacz [Przejdź połączonych zasobów](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Eksplorator usługi Storage platformy Azure
*Eksplorator usługi Storage Azure* stanowi przydatne narzędzie do sprawdzania i zmiany danych w obiektach blob. To narzędzie wolnego typu open source, który można pobrać z [http://storageexplorer.com/](http://storageexplorer.com/). Kod źródłowy jest dostępny z tego łącza, a także.

Przed użyciem tego narzędzia, musisz znać Azure klucz konta magazynu nazwy i konta. Aby uzyskać instrukcje dotyczące pobierania tych informacji, zobacz "jak: widoku, kopiowania i regenerate magazynu klucze dostępu" sekcji [tworzenia, zarządzania i usuwania konta magazynu][azure-create-storage-account].

1. Uruchom Eksploratora usługi Storage platformy Azure. Jeśli przy pierwszym uruchomieniu Eksploratora magazynu, zostanie wyświetlony monit dla **nazwa konta miej_sca VM** i **klucz konta magazynu**. Po uruchomieniu go przed użyj **Dodaj** przycisk, aby dodać nową nazwę konta magazynu i klucza.

    Wprowadź nazwę i klucza konta magazynu używane przez klaster usługi HDInsight, a następnie wybierz **Otwórz z & APISZ**.

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. Na liście kontenerów do lewej strony interfejsu kliknij nazwę kontenera, w którym jest skojarzony z klastrem usługi HDInsight. Domyślnie to jest nazwą klastra usługi HDInsight, ale mogą być inne, jeśli określona nazwa wprowadzona podczas tworzenia klastra.
3. Na pasku narzędzi wybierz ikonę przekazywania.

    ![Pasek narzędzi z ikoną przekazywania wyróżnione](./media/hdinsight-upload-data/toolbar.png)
4. Określ plik do przekazania, a następnie kliknij przycisk **Otwórz**. Po wyświetleniu monitu wybierz **przekazać** można przekazać pliku do katalogu głównego kontenera magazynu. Jeśli chcesz przekazać pliku do określonej ścieżki, wprowadź ścieżkę w **docelowego** a następnie wybierz opcję **przekazać**.

    ![Okno dialogowe przekazywania pliku](./media/hdinsight-upload-data/fileupload.png)

    Po zakończeniu przekazywania, można go użyć z zadań w klastrze usługi HDInsight.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Magazyn obiektów Blob Azure instalacji jako dysk lokalny
Zobacz [magazyn obiektów Blob Azure instalacji jako dysk lokalny](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Usługi
### <a name="azure-data-factory"></a>Azure Data Factory
Usługi fabryka danych Azure jest w pełni zarządzaną usługę służącą do tworzenia magazynu, przetwarzanie danych i danych usługi przenoszenia danych usługi w potokach produkcji prostsze, skalowalne i niezawodne danych.

Fabryka danych Azure może służyć do przenoszenia danych do magazynu obiektów Blob platformy Azure lub utworzyć potoki danych, które bezpośrednio przy użyciu funkcji usługi HDInsight, takich jak Hive i Pig.

Aby uzyskać więcej informacji, zobacz [dokumentacji fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop to narzędzie przeznaczone do transferu danych między Hadoop a relacyjnymi bazami danych. Można go użyć do importowania danych z systemu zarządzania relacyjnymi bazami danych (RDBMS), takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed (HDFS), Przekształć dane w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować dane do RDBMS.

Aby uzyskać więcej informacji, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>Programowanie zestawów SDK
Magazyn obiektów Blob Azure można również uzyskać dostęp za pomocą zestawu Azure SDK w następujących językach programowania:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Aby uzyskać więcej informacji na temat instalowania zestawów SDK usługi Azure, zobacz [Azure pliki do pobrania.](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a id="storageexception"></a>Wyjątek magazynu do zapisu dla obiektu blob
**Objawy**: przy użyciu `hadoop` lub `hdfs dfs` poleceń, aby zapisywać pliki, które są ~ 12 GB lub większej na klaster HBase, może wystąpić następujący błąd:

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Przyczyna**: HBase w usłudze HDInsight clusters domyślne do blok o rozmiarze 256 KB podczas zapisywania do magazynu Azure. Gdy działa to w przypadku interfejsu API REST lub interfejsów API HBase, spowoduje błąd przy użyciu `hadoop` lub `hdfs dfs` narzędzi wiersza polecenia.

**Rozdzielczość**: Użyj `fs.azure.write.request.size` do określ większy rozmiar bloku. Należy na podstawie użycia za pomocą `-D` parametru. Poniżej przedstawiono przykład użycia tego parametru z `hadoop` polecenia:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Można również zwiększyć wartość `fs.azure.write.request.size` globalnie, za pomocą narzędzia Ambari. Poniższe kroki można zmienić wartość w interfejsie użytkownika sieci Web Ambari:

1. W przeglądarce przejdź do Interfejsu sieci Web Ambari dla klastra. Jest to https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą klastra.

    Po wyświetleniu monitu wprowadź nazwę administratora i hasła dla klastra.
2. Po lewej stronie ekranu, wybierz **HDFS**, a następnie wybierz **Configs** kartę.
3. W **filtru...**  wprowadź `fs.azure.write.request.size`. Spowoduje to wyświetlenie pola i bieżąca wartość w środku strony.
4. Zmień wartość z 262144 (256KB) do nowej wartości. Na przykład 4194304 (4MB).

![Obraz zmiany wartości za pośrednictwem interfejsu użytkownika sieci Web Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Następne kroki
Teraz, gdy wiesz, jak można pobrać danych do usługi HDInsight, przeczytaj następujące artykuły, aby dowiedzieć się, jak wykonywać analizy:

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
