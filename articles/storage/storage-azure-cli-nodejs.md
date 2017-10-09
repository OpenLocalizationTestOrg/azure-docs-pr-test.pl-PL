---
title: "Witaj aaaUsing 1.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello interfejsu wiersza polecenia platformy Azure (Azure CLI) 1.0, z toocreate magazynu Azure i zarządzać kontami magazynu i pracować z plikami i obiekty BLOB platformy Azure. Hello Azure CLI jest narzędziem do wielu platform"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Przy użyciu hello Azure CLI 1.0 z usługą Azure Storage

## <a name="overview"></a>Omówienie

Hello wiersza polecenia platformy Azure oferuje zestaw typu open source, obsługujący wiele platform polecenia dotyczące pracy z hello platformy Azure. Zapewnia znacznie hello tę samą funkcjonalność znalezione w hello [portalu Azure](https://portal.azure.com) danych oraz jak sformatowanego dostęp do funkcji.

W tym przewodniku, firma Microsoft będzie Eksploruj jak toouse [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../cli-install-nodejs.md) tooperform różnych zadań programowania i administracji z usługą Azure Storage. Zalecamy, aby pobrać i zainstalować lub uaktualnić toohello najnowsze wiersza polecenia platformy Azure, przed rozpoczęciem korzystania z tego przewodnika.

W tym przewodniku założono, że rozumiesz hello podstawowych pojęciach dotyczących usługi Azure Storage. Przewodnik Hello zawiera liczby skryptów toodemonstrate użycie hello hello wiersza polecenia platformy Azure z usługą Azure Storage. Należy się tooupdate hello zmienne skryptu na podstawie konfiguracji przed uruchomieniem każdego skryptu.

> [!NOTE]
> Przewodnik Hello przedstawiono przykłady poleceń i skryptów wiersza polecenia platformy Azure hello klasycznych kont magazynu. Zobacz [hello Using Azure CLI for Mac, Linux i Windows z usługą Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) dla polecenia wiersza polecenia platformy Azure dla Menedżera zasobów konta magazynu.
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Wprowadzenie do usługi Azure Storage i hello wiersza polecenia platformy Azure w ciągu 5 minut
W tym przewodniku używa Ubuntu przykłady, ale innych platform systemu operacyjnego należy wykonać w podobny sposób.

**Nowe tooAzure:** subskrypcji Microsoft Azure i konta Microsoft skojarzonego z jego subskrypcją. Aby uzyskać informacje na temat opcji zakupu platformy Azure, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/), [opcjami zakupu](https://azure.microsoft.com/pricing/purchase-options/), i [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/) (dla członków MSDN, Microsoft Partner Network, BizSpark i innych programów firmy Microsoft).

Zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) uzyskać więcej informacji o subskrypcji platformy Azure.

**Po utworzeniu subskrypcji Microsoft Azure i konto:**

1. Pobierz i zainstaluj hello wiersza polecenia platformy Azure, postępując zgodnie z instrukcjami hello opisane w [hello instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).
2. Po hello wiersza polecenia platformy Azure został zainstalowany, będzie możliwe toouse hello azure polecenie z poleceń Azure CLI hello tooaccess interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia). Typ hello _azure_ polecenia i powinna zostać wyświetlona hello następujące dane wyjściowe.

    ![Dane wyjściowe polecenia platformy Azure][Image1]
3. W hello interfejsu wiersza polecenia, wpisz `azure storage` toolist całe hello polecenia magazynu azure i uzyskać pierwszy wrażenie Witaj Witaj funkcje interfejsu wiersza polecenia Azure udostępnia. Możesz wpisać nazwę polecenia z **-h** parametru (na przykład `azure storage share create -h`) toosee szczegóły składni polecenia.
4. Teraz przedstawimy prosty skrypt, który zawiera podstawowe tooaccess polecenia interfejsu wiersza polecenia Azure usługi Azure Storage. skrypt Hello najpierw zapyta tooset dwie zmienne dla konta magazynu i klucza. Następnie skryptu hello utworzyć nowy kontener w tym nowe konto magazynu i przekaż istniejącego kontenera toothat obrazu pliku (blob). Po skryptu hello znajduje się lista wszystkich obiektów blob w tym kontenerze, pobierze hello obrazu pliku toohello katalog docelowy która istnieje na komputerze lokalnym hello.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. W komputerze lokalnym Otwórz w edytorze tekstów preferowanych (vim na przykład). Typ hello powyżej skrypt do edytora tekstu.
6. Teraz należy zmienne skryptu hello tooupdate na podstawie własnych ustawień konfiguracji.

   * **< Storage_account_name >** Użyj hello otrzymuje nazwę w skrypcie hello, lub wprowadź nową nazwę dla konta magazynu. **Ważne:** hello nazwa konta magazynu hello musi być unikatowa na platformie Azure. Musi być pisane małymi literami, zbyt!
   * **< storage_account_key >** hello klucz dostępu konta magazynu.
   * **< Container_name >** Użyj hello otrzymuje nazwę w skrypcie hello lub wprowadź nową nazwę dla Twojego kontenera.
   * **< Image_to_upload >** wprowadź obraz tooa ścieżkę na komputerze lokalnym, na przykład: "~ / images/HelloWorld.png".
   * **< Destination_folder >** wprowadź ścieżkę tooa katalogu lokalnego toostore pliki pobierane z usługi Magazyn Azure, takich jak: "~/downloadImages".
7. Po zaktualizowaniu hello niezbędne zmiennych w vim naciśnij kombinacje klawiszy `ESC`, `:`, `wq!` toosave hello skryptu.
8. toorun ten skrypt, po prostu typu hello nazwę pliku skryptu w konsoli bash hello. Po uruchomieniu tego skryptu, ma lokalne miejsce docelowe folder, który zawiera hello pobrany plik obrazu. powitania po zrzut ekranu przedstawia przykład danych wyjściowych:

Po uruchomieniu skryptu hello powinien mieć folderu lokalne miejsce docelowe, który zawiera hello pobrany plik obrazu.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Zarządzanie kontami magazynu z hello wiersza polecenia platformy Azure
### <a name="connect-tooyour-azure-subscription"></a>Połącz tooyour subskrypcji platformy Azure
Większość poleceń magazynu hello będzie działać bez subskrypcji platformy Azure, ale zalecamy tooconnect tooyour subskrypcji z hello wiersza polecenia platformy Azure. tooconfigure hello Azure CLI toowork w ramach subskrypcji, wykonaj kroki hello w [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Utwórz nowe konto magazynu
toouse magazynu Azure, konieczne będzie konto magazynu. Po skonfigurowaniu subskrypcji tooyour tooconnect komputera, można utworzyć nowe konto magazynu platformy Azure.

```azurecli
azure storage account create <account_name>
```

Nazwa Hello konta magazynu musi mieć od 3 do 24 znaków i korzystać tylko cyfry i małe litery.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Ustaw domyślnego konta magazynu Azure w zmiennych środowiskowych
Może mieć wielu kont magazynu w ramach subskrypcji. Można wybrać jedną z nich i ustaw go w hello zmiennych środowiskowych dla wszystkich magazynu hello polecenia w hello sam sesji. Dzięki temu toorun hello Azure CLI magazynu polecenia bez określania magazynu hello konta i klucz jawnie.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Inny sposób tooset domyślne konto magazynu jest przy użyciu parametrów połączenia. Po pierwsze uzyskać hello parametry połączenia za pomocą polecenia:

```azurecli
azure storage account connectionstring show <account_name>
```

Następnie skopiuj parametry połączenia danych wyjściowych hello i ustaw zmienną tooenvironment:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Tworzenie i zarządzanie nimi obiektów blob
Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS. W tej sekcji założono, że znasz już pojęcia dotyczące magazynu obiektów Blob platformy Azure hello. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Tworzenie kontenera
Każdy obiekt blob w magazynie Azure musi być w kontenerze. Możesz utworzyć kontener prywatnego przy użyciu hello `azure storage container create` polecenia:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Istnieją trzy poziomy anonimowy dostęp do odczytu: **poza**, **obiektu Blob**, i **kontenera**. tooprevent anonimowego dostępu zbyt tooblobs, parametr uprawnienia hello zestawu**poza**. Domyślnie nowy kontener hello jest prywatny i jest możliwy tylko przez właściciela konta hello. odczytu tooallow publicznego anonimowy dostęp do zasobów tooblob, ale nie toocontainer metadanych lub toohello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**obiektu Blob**. tooallow publicznego Pełny odczyt dostęp do zasobów tooblob metadanych kontenera i hello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**kontenera**. Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob. Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload obiekty BLOB w kontenerze tooa, można użyć hello `azure storage blob upload`. Domyślnie to polecenie wysyła hello lokalne pliki tooa — obiekt blob blokowy. Typ hello toospecify hello obiektu blob, można użyć hello `--blobtype` parametru.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Pobierać obiekty BLOB z kontenera
Witaj poniższy przykład pokazuje, jak toodownload obiektów blob z kontenera.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Kopiowanie obiektów blob
Można asynchronicznie kopiować obiekty blob w obrębie konta magazynu i regionu lub między różnymi kontami magazynu i regionami.

Witaj poniższym przykładzie pokazano, jak obiekty BLOB toocopy z jednego magazynu konta tooanother. W tym przykładzie tworzymy kontenera, w których obiekty BLOB są publicznie, anonimowo dostępny.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

W tym przykładzie wykonuje asynchroniczne kopiowania. Możesz monitorować stan hello każdej operacji kopiowania, uruchamiając hello `azure storage blob copy show` operacji.

Należy pamiętać, że hello źródłowy adres URL podany dla operacji kopiowania hello musi być dostępny publicznie albo obejmuje tokenu sygnatury dostępu Współdzielonego (sygnatury dostępu współdzielonego).

### <a name="delete-a-blob"></a>Usuwanie obiektu blob
toodelete obiektu blob, użyj hello poniżej polecenia:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Tworzenie i Zarządzanie udziałami plików
Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających standardowego protokołu SMB hello. Maszyny wirtualne Microsoft Azure i usługi w chmurze, a także aplikacje lokalne mogą udostępniać dane za pośrednictwem zainstalowanych udziałów. Możesz zarządzać udziałami plików i danych plików za pośrednictwem hello Azure CLI. Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](storage-dotnet-how-to-use-files.md) lub [jak toouse magazyn plików Azure z systemem Linux](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Tworzenie udziału plików
Udział plików Azure jest udziałem plików SMB na platformie Azure. Wszystkie pliki i katalogi, należy utworzyć w udziale plików. Konto może zawierać nieograniczoną liczbę udziałów, a udział może przechowywać nieograniczoną liczbę plików w górę toohello limity pojemności konta magazynu hello. Witaj poniższy przykład tworzy udział plików o nazwie **moj_udzial**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Tworzenie katalogu
Katalog udostępnia opcjonalne strukturę hierarchiczną do udziału plików na platformę Azure. Witaj poniższy przykład tworzy katalog o nazwie **myDir** w hello udziału plików.

```azurecli
azure storage directory create myshare myDir
```

Należy pamiętać, że ścieżki katalogu może zawierać wiele poziomów *np.*, **/ b**. Należy jednak upewnij się, że istnieją wszystkie katalogi nadrzędne. Na przykład dla ścieżki **/ b**, należy utworzyć katalog **** najpierw utwórz katalog **b**.

### <a name="upload-a-local-file-toodirectory"></a>Przekaż toodirectory pliku lokalnego
Witaj poniższym przykładzie plik zostanie przekazany z **~/temp/samplefile.txt** toohello **myDir** katalogu. Edytuj hello ścieżkę pliku tak, aby wskazywało tooa prawidłowy plik na komputerze lokalnym:

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Należy pamiętać, że plik w udziale hello może być zapasowej TB too1 rozmiar.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Wyświetlanie listy plików hello w katalogu głównego udziału hello lub katalogu
Możesz wyświetlić listę hello pliki i podkatalogi w katalogu głównego udziału lub w katalogu przy użyciu hello następujące polecenie:

```azurecli
azure storage file list myshare myDir
```

Należy pamiętać, że podana nazwa katalogu hello jest opcjonalny w przypadku hello listę operacji. Pominięcie hello polecenie wyświetla listę hello zawartość katalogu głównego hello hello udziału.

### <a name="copy-files"></a>Kopiowanie plików
Począwszy od wersji 0.9.8 wiersza polecenia platformy Azure, można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob. Poniżej przedstawiamy, jak tooperform je skopiować operacji za pomocą polecenia interfejsu wiersza polecenia. toocopy nowy katalog toohello pliku:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy katalogu plików tooa obiektu blob:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Następne kroki

Dokumentacja poleceń Azure 1.0 interfejsu wiersza polecenia można znaleźć do pracy z zasobami magazynu w tym miejscu:

* [Azure polecenia interfejsu wiersza polecenia w trybie Menedżera zasobów](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Azure polecenia interfejsu wiersza polecenia w trybie zarządzania usługami Azure](../cli-install-nodejs.md)

Również chcesz tootry hello [Azure CLI 2.0](storage-azure-cli.md), naszych CLI generacji napisane w języku Python, do użycia z modelu wdrażania usługi Resource Manager hello.

[Image1]: ./media/storage-azure-cli/azure_command.png
