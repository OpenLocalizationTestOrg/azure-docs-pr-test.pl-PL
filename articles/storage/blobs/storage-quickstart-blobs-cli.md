---
title: "Szybki start platformy Azure — Transferowanie obiektów do usługi Azure Blob Storage i z niej za pomocą interfejsu wiersza polecenia platformy Azure | Microsoft Docs"
description: "Skrócona instrukcja transferowania obiektów do usługi Azure Blob Storage i z niej za pomocą interfejsu wiersza polecenia platformy Azure"
services: storage
documentationcenter: na
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/19/2017
ms.author: tamram
ms.openlocfilehash: 7313df35baadf7aa6d476f44b113dc60e6845f4b
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="transfer-objects-tofrom-azure-blob-storage-using-the-azure-cli"></a>Transferowanie obiektów do usługi Azure Blob Storage i z niej za pomocą interfejsu wiersza polecenia platformy Azure

Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów. Ten przewodnik Szybki start zawiera opis wykorzystania interfejsu wiersza polecenia platformy Azure do przesyłania danych do/z usługi Azure Blob Storage.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten przewodnik szybkiego startu będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0](/cli/azure/install-azure-cli).

[!INCLUDE [storage-quickstart-tutorial-intro-include-cli](../../../includes/storage-quickstart-tutorial-intro-include-cli.md)]

## <a name="create-a-container"></a>Tworzenie kontenera

Obiekty blob są zawsze przesyłane do kontenera. Możesz organizować grupy obiektów blob w sposób podobny do organizowania plików w folderach na komputerze.

Do tworzenia kontenera do przechowywania obiektów blob służy polecenie [az storage container create](/cli/azure/storage/container#create).

```azurecli-interactive
az storage container create --name mystoragecontainer
```

## <a name="upload-a-blob"></a>Przesyłanie obiektów blob

Usługa Blob Storage obsługuje blokowe, uzupełnialne i stronicowe obiekty blob. Większość plików przechowywanych w usłudze Blob Storage jest przechowywana jako blokowe obiekty blob. Uzupełnialne obiekty blob są używane w razie konieczności dodania danych do istniejącego obiektu blob bez modyfikowania jego zawartości, na przykład w przypadku rejestrowania. Stronicowe obiekty blob obsługują pliki VHD maszyn wirtualnych IaaS.

Najpierw utwórz plik do przekazania do obiektu blob.
Jeśli używasz usługi Azure Cloud Shell, utwórz plik za pomocą następującego polecenia: `vi helloworld` po otwarciu pliku, naciśnij klawisz **Insert**, wpisz „Hello wrold”, a następnie naciśnij klawisz **Esc**, wpisz `:x` i naciśnij klawisz **Enter**.

W tym przykładzie do kontenera utworzonego w ostatnim kroku zostanie przekazany obiekt blob za pomocą polecenia [az storage blob upload](/cli/azure/storage/blob#upload).

```azurecli-interactive
az storage blob upload \
    --container-name mystoragecontainer \
    --name blobName \
    --file ~/path/to/local/file
```

Jeśli w usłudze Azure Cloud Shell utworzono plik przy użyciu wcześniej opisanej metody, możesz zamiast tego użyć następującego polecenia interfejsu wiersza polecenia (zauważ, że nie trzeba było podawać ścieżki, ponieważ plik utworzono w katalogu podstawowym; zazwyczaj podanie ścieżki jest konieczne):

```azurecli-interactive
az storage blob upload \
    --container-name mystoragecontainer \
    --name helloworld
    --file helloworld
```

Jeśli obiekt blob nie istnieje, zostanie utworzony. W przeciwnym razie zostanie zastąpiony. Przed kontynuowaniem można przesłać dowolną liczbę plików.

Aby przekazać jednocześnie wiele plików, możesz użyć polecenia [az storage blob upload-batch](/cli/azure/storage/blob#upload-batch).

## <a name="list-the-blobs-in-a-container"></a>Wyświetlanie listy obiektów blob w kontenerze

Do wyświetlania listy obiektów blob w kontenerze służy polecenie [az storage blob list](/cli/azure/storage/blob#list).

```azurecli-interactive
az storage blob list \
    --container-name mystoragecontainer \
    --output table
```

## <a name="download-a-blob"></a>Pobieranie obiektu blob

Użyj polecenia [az storage blob download](/cli/azure/storage/blob#download), aby pobrać przesłany wcześniej obiekt blob.

```azurecli-interactive
az storage blob download \
    --container-name mystoragecontainer \
    --name blobName \
    --file ~/destination/path/for/file
```

## <a name="data-transfer-with-azcopy"></a>Transfer danych przy użyciu narzędzia AzCopy

Narzędzie [AzCopy](../common/storage-use-azcopy-linux.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) to kolejna opcja umożliwiająca wydajny transfer danych do usługi Azure Storage z użyciem skryptów. Narzędzia AzCopy można używać do transferu danych do i z magazynu obiektów blob, plików i tabel.

Oto przykładowe polecenie AzCopy umożliwiające przesłanie pliku o nazwie *myfile.txt* do kontenera *mystoragecontainer*.

```bash
azcopy \
    --source /mnt/myfiles \
    --destination https://mystorageaccount.blob.core.windows.net/mystoragecontainer \
    --dest-key <storage-account-access-key> \
    --include "myfile.txt"
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie są już potrzebne żadne zasoby z grupy zasobów, w tym konto magazynu utworzone w ramach tego przewodnika Szybki start, usuń grupę zasobów za pomocą polecenia [az group delete](/cli/azure/group#delete).

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start przedstawiono metodę transferowania plików między dyskiem lokalnym i kontenerem w usłudze Azure Blob Storage. Aby dowiedzieć się więcej na temat pracy z obiektami blob w usłudze Azure Storage, przejdź do samouczka dotyczącego pracy z usługą Azure Blob Storage.

> [!div class="nextstepaction"]
> [Instrukcje: operacje przeprowadzane w usłudze Blob Storage przy użyciu interfejsu wiersza polecenia platformy Azure](storage-how-to-use-blobs-cli.md)
