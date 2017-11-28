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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="1151a-103">Utwórz udział plików w usłudze Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="1151a-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="1151a-104">Można utworzyć udziały plików platformy Azure przy użyciu [portalu Azure](https://portal.azure.com/)hello poleceń cmdlet programu PowerShell magazynu Azure, hello biblioteki klienta magazynu Azure albo hello interfejsu API REST magazynu Azure. Z tego samouczka dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="1151a-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="1151a-105">Jak udostępnić toocreate plików platformy Azure przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1151a-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="1151a-106">Jak toocreate Azure udział plików przy użyciu programu Powershell</span><span class="sxs-lookup"><span data-stu-id="1151a-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="1151a-107">Jak toocreate Azure udział plików przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="1151a-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="1151a-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1151a-108">Prerequisites</span></span>
<span data-ttu-id="1151a-109">toocreate udziału plików platformy Azure, korzystając z konta magazynu, który już istnieje, lub [Utwórz nowe konto magazynu Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1151a-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="1151a-110">toocreate udziału plików platformy Azure przy użyciu programu PowerShell, konieczne będzie hello klucz konta i nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1151a-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="1151a-111">Jeśli planujesz toouse programu Powershell lub interfejsu wiersza polecenia, należy klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1151a-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="1151a-112">Tworzenie udziału plików za pośrednictwem hello portalu</span><span class="sxs-lookup"><span data-stu-id="1151a-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="1151a-113">**Blok konta tooStorage Przejdź w portalu Azure**:</span><span class="sxs-lookup"><span data-stu-id="1151a-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="1151a-114">![Blok Konto magazynu](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="1151a-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="1151a-115">**Kliknij przycisk Dodaj udział pliku**:</span><span class="sxs-lookup"><span data-stu-id="1151a-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="1151a-116">![Kliknij przycisk hello Dodawanie przycisku udziału plików](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="1151a-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="1151a-117">**Podaj nazwę i limit przydziału. Obecnie maksymalna wartość przydziału wynosi 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="1151a-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="1151a-118">![Podaj nazwę i żądany przydział hello nowego udziału plików](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="1151a-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="1151a-119">**Wyświetl nowy udział plików**: ![Wyświetl swój nowy udział plików](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="1151a-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="1151a-120">**Przekaż plik**: ![Przekaż plik](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="1151a-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="1151a-121">**Przejdź do udziału plików i zarządzaj swoimi plikami i katalogami**: ![Przeglądaj udział plików](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="1151a-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="1151a-122">Tworzenie udziału plików za pośrednictwem programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1151a-122">Create file share through PowerShell</span></span>
<span data-ttu-id="1151a-123">toouse tooprepare programu PowerShell, Pobierz i zainstaluj polecenia cmdlet programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1151a-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="1151a-124">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) hello zainstalować instrukcje instalacji i punktu.</span><span class="sxs-lookup"><span data-stu-id="1151a-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="1151a-125">Zaleca się pobrać i zainstalować lub uaktualnić toohello najnowsze modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1151a-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="1151a-126">**Tworzenie kontekstu konta magazynu i klucza** kontekstu hello hermetyzuje hello magazynu konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="1151a-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="1151a-127">Aby uzyskać instrukcje dotyczące kopiowania klucza konta z witryny [Azure Portal](https://portal.azure.com/), zobacz [Wyświetlanie i kopiowanie kluczy dostępu do magazynu](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="1151a-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="1151a-128">**Utwórz nowy udział plików**:</span><span class="sxs-lookup"><span data-stu-id="1151a-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="1151a-129">Witaj nazwa udziału plików musi być tylko małe litery.</span><span class="sxs-lookup"><span data-stu-id="1151a-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="1151a-130">Szczegółowe informacje o nazwach plików i udziałów plików można znaleźć w temacie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Nazywanie i odwoływanie się do udziałów, katalogów, plików i metadanych).</span><span class="sxs-lookup"><span data-stu-id="1151a-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="1151a-131">Tworzenie udziału plików za pomocą interfejsu wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="1151a-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="1151a-132">**toouse tooprepare interfejsu wiersza polecenia (CLI), Pobierz i zainstaluj hello wiersza polecenia platformy Azure.**</span><span class="sxs-lookup"><span data-stu-id="1151a-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="1151a-133">Zobacz artykuły [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0) i [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) (Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure w wersji 2.0).</span><span class="sxs-lookup"><span data-stu-id="1151a-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="1151a-134">**Tworzenie konta magazynu toohello ciąg połączenia, w którym ma toocreate hello udziału.**</span><span class="sxs-lookup"><span data-stu-id="1151a-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="1151a-135">Zastąp ```<storage-account>``` i ```<resource_group>``` z Twojego konta nazwy i zasobów grupy magazynów w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="1151a-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="1151a-136">**Tworzenie udziału plików**</span><span class="sxs-lookup"><span data-stu-id="1151a-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="1151a-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1151a-137">Next steps</span></span>
* [<span data-ttu-id="1151a-138">Łączenie i instalowanie udziału plików — system Windows</span><span class="sxs-lookup"><span data-stu-id="1151a-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="1151a-139">Łączenie i instalowanie udziału plików — system Linux</span><span class="sxs-lookup"><span data-stu-id="1151a-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="1151a-140">Łączenie i instalowanie udziału plików — system macOS</span><span class="sxs-lookup"><span data-stu-id="1151a-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="1151a-141">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="1151a-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="1151a-142">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="1151a-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="1151a-143">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="1151a-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)