---
title: "Witaj aaaUsing 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello interfejsu wiersza polecenia platformy Azure (Azure CLI) 2.0, o toocreate magazynu Azure i zarządzanie kontami magazynu i pracować z plikami i obiekty BLOB platformy Azure. Hello Azure CLI 2.0 to narzędzie i platform napisanych w języku Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage

Hello open source, 2.0 interfejsu wiersza polecenia platformy Azure i platform udostępnia zestaw poleceń do pracy z hello platformy Azure. Zapewnia znacznie hello tę samą funkcjonalność znalezione w hello [portalu Azure](https://portal.azure.com), w tym dostęp do zaawansowanych danych.

W tym przewodniku zostanie przedstawiony zostanie sposób toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform kilka zadań, Praca z zasobów na koncie magazynu Azure. Zaleca się pobrać i zainstalować lub uaktualnić toohello najnowszą wersję hello 2.0 interfejsu wiersza polecenia przed rozpoczęciem korzystania z tego przewodnika.

Przykłady Hello w przewodniku hello założono użycie hello hello powłoki Bash na Ubuntu, ale innych platform, należy wykonać podobnie. 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku założono, że rozumiesz hello podstawowych pojęciach dotyczących usługi Azure Storage. Przyjęto założenie, że jesteś toosatisfy stanie hello tworzenie wymagania dotyczące konta określonych poniżej platformy Azure i hello usługi magazynu.

### <a name="accounts"></a>Konta
* **Konto platformy Azure**: Jeśli nie masz już subskrypcję platformy Azure, [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).
* **Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Zainstaluj hello Azure CLI 2.0

Pobierz i zainstaluj hello Azure CLI 2.0, wykonując instrukcje hello opisane w temacie [zainstalować Azure CLI 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Jeśli masz problemy z instalacją hello, zapoznaj się hello [Rozwiązywanie problemów z instalacji](/cli/azure/install-az-cli2#installation-troubleshooting) części artykułu hello i hello [zainstalować Rozwiązywanie problemów z](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) przewodnik w witrynie GitHub.
>

## <a name="working-with-hello-cli"></a>Praca z hello interfejsu wiersza polecenia

Po zainstalowaniu hello interfejsu wiersza polecenia, można użyć hello `az` polecenia w poleceniach wiersza polecenia platformy Azure hello tooaccess interfejsu wiersza polecenia (Bash, Terminal wiersza polecenia). Typ hello `az` toosee polecenia pełną listę poleceń podstawowej hello (hello następujące przykładowe dane wyjściowe zostały obcięte):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

W interfejsie wiersza polecenia, wykonaj polecenie hello `az storage --help` toolist hello `storage` polecenia podgrup. opisy Hello podgrupy hello omówiono hello powitalne funkcji interfejsu wiersza polecenia Azure zapewnia do pracy z zasobami magazynu.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Połącz hello CLI tooyour subskrypcji platformy Azure

toowork hello zasobów w Twojej subskrypcji platformy Azure, musisz najpierw zalogować się tooyour konto platformy Azure z `az login`. Istnieje kilka metod, które możesz zalogować się:

* **Logowanie interakcyjne**:`az login`
* **Zaloguj się przy użyciu nazwy użytkownika i hasła**:`az login -u johndoe@contoso.com -p VerySecret`
  * To nie działa z konta Microsoft lub konta, które korzystają z uwierzytelniania wieloskładnikowego.
* **Zaloguj się przy użyciu nazwy głównej usługi**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Azure CLI 2.0 przykładowy skrypt

Następnie będzie pracujemy ze skryptem małych powłoki, który wystawia kilka podstawowych toointeract poleceń Azure CLI 2.0 z zasobami magazynu platformy Azure. skrypt Hello najpierw tworzy nowy kontener na koncie magazynu, a następnie przekazuje istniejącego kontenera toothat pliku (jako obiektu blob). Wyświetla listę wszystkich obiektów blob w kontenerze hello, a na koniec pobiera hello pliku tooa docelowego na komputerze lokalnym, który określisz.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Skonfiguruj i uruchom skrypt hello**

1. Otwórz w ulubionym edytorze tekstów, a następnie skopiuj i Wklej hello poprzedzających skrypt do edytora hello.

2. Następnie zaktualizuj tooreflect zmienne skryptu hello ustawień konfiguracji. Zastąp następujące wartości określonych hello:

   * **\<storage_account_name\>**  hello nazwę konta magazynu.
   * **\<storage_account_key\>**  hello klucz podstawowy lub pomocniczy dostępu dla konta magazynu.
   * **\<container_name\>**  nazwę hello nowy kontener toocreate, takie jak "azure-cli — próbki container".
   * **\<blob_name\>**  nazwę hello docelowego obiektu blob w kontenerze hello.
   * **\<file_to_upload\>**  hello ścieżki pliku toosmall na komputerze lokalnym, takich jak "~ / images/HelloWorld.png".
   * **\<destination_file\>**  hello ścieżkę pliku docelowego, takich jak "~ / downloadedImage.png".

3. Po zaktualizowaniu zmienne niezbędne hello zapisać skrypt hello, a następnie zamknij Edytor. Następne kroki Hello założono nazwanego skryptu **my_storage_sample.sh**.

4. Oznacz hello skrypt jako plik wykonywalny, w razie potrzeby:`chmod +x my_storage_sample.sh`

5. Uruchom skrypt hello. Na przykład w Bash:`./my_storage_sample.sh`

Należy znaleźć dane wyjściowe podobne toohello w następujących tematach i hello  **\<destination_file\>**  określone w hello skryptu powinny pojawiać się na komputerze lokalnym.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Witaj Powyższy wynik znajduje się w **tabeli** format. Można określić wyjściowy, który format toouse określając hello `--output` argument w poleceniach interfejsu wiersza polecenia lub ustaw ją za pomocą `az configure`.
>

## <a name="manage-storage-accounts"></a>Zarządzanie kontami magazynu

### <a name="create-a-new-storage-account"></a>Utwórz nowe konto magazynu
toouse magazynu Azure, musisz mieć konto magazynu. Można utworzyć nowe konto magazynu Azure, po skonfigurowaniu komputera za[połączenia subskrypcji tooyour](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location`[Wymagane]: lokalizacji. Na przykład "zachodnie stany USA".
* `--name`[Wymagane]: Nazwa konta magazynu hello. Witaj nazwa musi składać się z 3 znaków too24 i używaj tylko małych znaków alfanumerycznych.
* `--resource-group`[Wymagane]: Nazwa grupy zasobów.
* `--sku`[Wymagane]: hello konta magazynu wersji. Dozwolone wartości:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Ustaw zmienne środowiskowe domyślne konto magazynu Azure
Może mieć wielu kont magazynu w ramach subskrypcji platformy Azure. tooselect jeden z nich polecenia toouse dla wszystkich kolejnych magazynu, można ustawić zmienne środowiskowe:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Inny sposób tooset domyślne konto magazynu jest przy użyciu ciągu połączenia. Najpierw pobierz hello ciągu połączenia za pomocą hello `show-connection-string` polecenia:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Następnie hello kopiowania danych wyjściowych ciąg połączenia i ustaw hello `AZURE_STORAGE_CONNECTION_STRING` zmiennej środowiskowej (może być konieczne w cudzysłów ciągu połączenia hello tooenclose):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Wszystkie przykłady w hello następujące sekcje w tym artykule założono, że ustawiono hello `AZURE_STORAGE_ACCOUNT` i `AZURE_STORAGE_ACCESS_KEY` zmiennych środowiskowych.
>

## <a name="create-and-manage-blobs"></a>Tworzenie i zarządzanie nimi obiektów blob
Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS. W tej sekcji założono, że znasz już pojęcia dotyczące magazynu obiektów Blob platformy Azure. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Tworzenie kontenera
Każdy obiekt blob w magazynie Azure musi być w kontenerze. Kontener można utworzyć przy użyciu hello `az storage container create` polecenia:

```azurecli
az storage container create --name <container_name>
```

Można ustawić jedną z trzech poziomów dostępu do odczytu dla nowego kontenera, określając hello opcjonalne `--public-access` argumentu:

* `off`(domyślnie): dane w kontenerze są prywatne toohello właściciela konta.
* `blob`: Publiczny dostęp do odczytu obiektów blob.
* `container`: Odczyt publiczny i listy dostępu toohello całego kontenera.

Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Przekaż tooa kontenera obiektów blob
Azure Blob storage obsługuje blok, Dołącz i stronicowe. Przekazywanie obiektów blob kontenera tooa przy użyciu hello `blob upload` polecenia:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Domyślnie program hello `blob upload` polecenia przekazuje obiekty BLOB toopage pliki *.vhd lub blokowych obiektów blob w inny sposób. toospecify innego typu kiedy przekazywanie obiektu blob, możesz użyć hello `--type` argumentu--dozwolone wartości są `append`, `block`, i `page`.

 Aby uzyskać więcej informacji o typach inny obiektu blob hello, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Pobieranie obiektu blob z kontenera
W tym przykładzie pokazano, jak toodownload obiektu blob z kontenera:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze

Wyświetlanie obiektów blob hello w kontenerze o hello [az magazynu obiektów blob listy](/cli/azure/storage/blob#list) polecenia.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Kopiowanie obiektów blob
Można asynchronicznie kopiować obiekty blob w obrębie konta magazynu i regionu lub między różnymi kontami magazynu i regionami.

Witaj poniższym przykładzie pokazano, jak obiekty BLOB toocopy z jednego magazynu konta tooanother. Najpierw utworzymy kontenera na koncie magazynu źródłowego hello, określając publiczny dostęp do odczytu do jego obiektów blob. Następnie możemy przekazać kontenera toohello plików, a na końcu obiektu blob hello kopiowania z tego kontenera do kontenera na koncie magazynu docelowego hello.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

W hello powyżej przykładzie hello docelowy kontener musi już istnieć w hello konto magazynu docelowego dla toosucceed operacji kopiowania hello. Ponadto hello źródłowego obiektu blob określone w hello `--source-uri` argument musi zawierać token sygnatury dostępu Współdzielonego dostępu współdzielonego, albo być dostępny publicznie, jak w poniższym przykładzie.

### <a name="delete-a-blob"></a>Usuwanie obiektu blob
toodelete obiektu blob, użyj hello `blob delete` polecenia:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Tworzenie i Zarządzanie udziałami plików
Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających protokołu bloku komunikatów serwera (SMB) hello. Maszyny wirtualne Microsoft Azure i usługi w chmurze, a także aplikacje lokalne mogą udostępniać dane za pośrednictwem zainstalowanych udziałów. Możesz zarządzać udziałami plików i danych plików za pośrednictwem hello Azure CLI. Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage-dotnet-how-to-use-files.md) lub [jak toouse magazyn plików Azure z systemem Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Tworzenie udziału plików
Udział plików Azure jest udziałem plików SMB na platformie Azure. Wszystkie pliki i katalogi, należy utworzyć w udziale plików. Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików w górę toohello limity pojemności konta magazynu hello. Witaj poniższy przykład tworzy udział plików o nazwie **moj_udzial**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Tworzenie katalogu
Katalog udostępnia strukturę hierarchiczną w udziale plików na platformę Azure. Witaj poniższy przykład tworzy katalog o nazwie **myDir** w hello udziału plików.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Ścieżki katalogu może zawierać wiele poziomów, na przykład **katalog1/dir2**. Należy jednak upewnij się, że wszystkie katalogi nadrzędne istnieć przed utworzeniem podkatalogu. Na przykład dla ścieżki **katalog1/dir2**, należy najpierw utworzyć katalog **katalog1**, następnie utwórz katalog **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Przekaż udziału tooa pliku lokalnego
Witaj poniższym przykładzie plik zostanie przekazany z **~/temp/samplefile.txt** tooroot hello **moj_udzial** udziału plików. Witaj `--source` argument określa hello istniejących tooupload pliku lokalnego.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Podobnie jak w przypadku tworzenia katalogu, można określić ścieżkę katalogu w ramach hello udziału tooupload hello tooan istniejącego katalogu pliku w udziale hello:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Plik w udziale hello można się too1 TB rozmiar.

### <a name="list-hello-files-in-a-share"></a>Wyświetlanie listy plików hello w udziale
Można wyświetlić listę plików i katalogów w udziale, za pomocą hello `az storage file list` polecenia:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Kopiowanie plików      
Można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob. Na przykład toocopy katalogu tooa plików w różnych udziału:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Następne kroki
Poniżej przedstawiono dodatkowe zasoby dowiedzieć się więcej o pracy z hello Azure CLI 2.0.

* [Wprowadzenie do usługi Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Dokumentacja poleceń interfejsu wiersza polecenia platformy Azure 2.0](/cli/azure)
* [Azure CLI 2.0 w witrynie GitHub](https://github.com/Azure/azure-cli)
