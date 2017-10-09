---
title: "toocreate aaaHow udział plików Azure | Dokumentacja firmy Microsoft"
description: "Jak toocreate Azure udział plików w usłudze magazyn plików Azure przy użyciu hello portalu Azure, programu PowerShell i hello wiersza polecenia platformy Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Utwórz udział plików w usłudze Azure File Storage
Można utworzyć udziały plików platformy Azure przy użyciu [portalu Azure](https://portal.azure.com/)hello poleceń cmdlet programu PowerShell magazynu Azure, hello biblioteki klienta magazynu Azure albo hello interfejsu API REST magazynu Azure. Z tego samouczka dowiesz się:
* [Jak udostępnić toocreate plików platformy Azure przy użyciu hello portalu Azure](#Create file share through hello Portal)
* [Jak toocreate Azure udział plików przy użyciu programu Powershell](#Create file share using PowerShell)
* [Jak toocreate Azure udział plików przy użyciu interfejsu wiersza polecenia](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Wymagania wstępne
toocreate udziału plików platformy Azure, korzystając z konta magazynu, który już istnieje, lub [Utwórz nowe konto magazynu Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json). toocreate udziału plików platformy Azure przy użyciu programu PowerShell, konieczne będzie hello klucz konta i nazwę konta magazynu. Jeśli planujesz toouse programu Powershell lub interfejsu wiersza polecenia, należy klucz konta magazynu.

## <a name="create-file-share-through-hello-portal"></a>Tworzenie udziału plików za pośrednictwem hello portalu
1. **Blok konta tooStorage Przejdź w portalu Azure**:    
    ![Blok Konto magazynu](./media/storage-how-to-create-file-share/create-file-share-portal1.png)

2. **Kliknij przycisk Dodaj udział pliku**:    
    ![Kliknij przycisk hello Dodawanie przycisku udziału plików](./media/storage-how-to-create-file-share/create-file-share-portal2.png)

3. **Podaj nazwę i limit przydziału. Obecnie maksymalna wartość przydziału wynosi 5 TB**:    
    ![Podaj nazwę i żądany przydział hello nowego udziału plików](./media/storage-how-to-create-file-share/create-file-share-portal3.png)

4. **Wyświetl nowy udział plików**: ![Wyświetl swój nowy udział plików](./media/storage-how-to-create-file-share/create-file-share-portal4.png)

5. **Przekaż plik**: ![Przekaż plik](./media/storage-how-to-create-file-share/create-file-share-portal5.png)

6. **Przejdź do udziału plików i zarządzaj swoimi plikami i katalogami**: ![Przeglądaj udział plików](./media/storage-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Tworzenie udziału plików za pośrednictwem programu PowerShell
toouse tooprepare programu PowerShell, Pobierz i zainstaluj polecenia cmdlet programu Azure PowerShell hello. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) hello zainstalować instrukcje instalacji i punktu.

> [!Note]  
> Zaleca się pobrać i zainstalować lub uaktualnić toohello najnowsze modułu Azure PowerShell.

1. **Tworzenie kontekstu konta magazynu i klucza** kontekstu hello hermetyzuje hello magazynu konta nazwy i klucza konta. Aby uzyskać instrukcje dotyczące kopiowania klucza konta z witryny [Azure Portal](https://portal.azure.com/), zobacz [Wyświetlanie i kopiowanie kluczy dostępu do magazynu](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Utwórz nowy udział plików**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> Witaj nazwa udziału plików musi być tylko małe litery. Szczegółowe informacje o nazwach plików i udziałów plików można znaleźć w temacie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Nazywanie i odwoływanie się do udziałów, katalogów, plików i metadanych).

## <a name="create-file-share-through-command-line-interface-cli"></a>Tworzenie udziału plików za pomocą interfejsu wiersza polecenia (CLI)
1. **toouse tooprepare interfejsu wiersza polecenia (CLI), Pobierz i zainstaluj hello wiersza polecenia platformy Azure.**  
    Zobacz artykuły [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0) i [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) (Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure w wersji 2.0).

2. **Tworzenie konta magazynu toohello ciąg połączenia, w którym ma toocreate hello udziału.**  
    Zastąp ```<storage-account>``` i ```<resource_group>``` z Twojego konta nazwy i zasobów grupy magazynów w hello poniższy przykład.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Tworzenie udziału plików**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Następne kroki
* [Łączenie i instalowanie udziału plików — system Windows](storage-how-to-use-files-windows.md)
* [Łączenie i instalowanie udziału plików — system Linux](../storage-how-to-use-files-linux.md)
* [Łączenie i instalowanie udziału plików — system macOS](storage-how-to-use-files-mac.md)

Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów w systemie Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Rozwiązywanie problemów w systemie Linux](storage-troubleshoot-linux-file-connection-problems.md)   