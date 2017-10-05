---
title: "Jak zarządzać usługą Azure File Storage za pomocą programu PowerShell | Microsoft Docs"
description: "Dowiedz się, jak zarządzać usługą Azure File Storage za pomocą programu PowerShell."
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
ms.openlocfilehash: 148375b156c4ae1aa4bf203d215f7ed607a71b89
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="16e66-103">Jak zarządzać usługą Azure File Storage za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="16e66-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="16e66-104">Przy użyciu programu Azure PowerShell można tworzyć udziały plików i zarządzać nimi.</span><span class="sxs-lookup"><span data-stu-id="16e66-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="16e66-105">Instalowanie poleceń cmdlet programu PowerShell dla usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="16e66-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="16e66-106">Aby przygotować się do użycia programu Azure PowerShell, pobierz i zainstaluj polecenia cmdlet tego programu.</span><span class="sxs-lookup"><span data-stu-id="16e66-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="16e66-107">Aby uzyskać informacje o punkcie instalacji oraz instrukcje dotyczące instalacji, zobacz [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Jak zainstalować i skonfigurować program Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="16e66-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="16e66-108">Zalecamy pobranie i zainstalowanie najnowszej wersji modułu Azure PowerShell (lub uaktualnienie do tej wersji).</span><span class="sxs-lookup"><span data-stu-id="16e66-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="16e66-109">Otwórz okno programu Azure PowerShell, klikając przycisk **Start** i wpisując polecenie **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="16e66-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="16e66-110">W oknie programu PowerShell zostanie załadowany moduł Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16e66-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="16e66-111">Tworzenie kontekstu konta magazynu i klucza</span><span class="sxs-lookup"><span data-stu-id="16e66-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="16e66-112">Utwórz kontekst konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="16e66-112">Create the storage account context.</span></span> <span data-ttu-id="16e66-113">W kontekście zawarta jest nazwa konta magazynu oraz klucz konta.</span><span class="sxs-lookup"><span data-stu-id="16e66-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="16e66-114">Aby uzyskać instrukcje dotyczące kopiowania klucza konta z witryny [Azure Portal](https://portal.azure.com), zobacz [Wyświetlanie i kopiowanie kluczy dostępu do magazynu](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="16e66-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="16e66-115">W poniższym przykładzie zastąp zmienne `storage-account-name` i `storage-account-key` nazwą konta magazynu i kluczem.</span><span class="sxs-lookup"><span data-stu-id="16e66-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="16e66-116">Tworzenie nowego udziału plików</span><span class="sxs-lookup"><span data-stu-id="16e66-116">Create a new file share</span></span>
<span data-ttu-id="16e66-117">Utwórz nowy udział o nazwie `logs`.</span><span class="sxs-lookup"><span data-stu-id="16e66-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="16e66-118">Masz już udział plików w usłudze Magazyn plików.</span><span class="sxs-lookup"><span data-stu-id="16e66-118">You now have a file share in File storage.</span></span> <span data-ttu-id="16e66-119">Teraz dodamy katalog i plik.</span><span class="sxs-lookup"><span data-stu-id="16e66-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16e66-120">Nazwa udziału plików musi się składać z samych małych liter.</span><span class="sxs-lookup"><span data-stu-id="16e66-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="16e66-121">Szczegółowe informacje o nazwach plików i udziałów plików można znaleźć w temacie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Nazywanie i odwoływanie się do udziałów, katalogów, plików i metadanych).</span><span class="sxs-lookup"><span data-stu-id="16e66-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="16e66-122">Tworzenie katalogu w udziale plików</span><span class="sxs-lookup"><span data-stu-id="16e66-122">Create a directory in the file share</span></span>
<span data-ttu-id="16e66-123">Utwórz katalog w udziale.</span><span class="sxs-lookup"><span data-stu-id="16e66-123">Create a directory in the share.</span></span> <span data-ttu-id="16e66-124">W poniższym przykładzie katalog nosi nazwę `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="16e66-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="16e66-125">Przekazywanie pliku lokalnego do katalogu</span><span class="sxs-lookup"><span data-stu-id="16e66-125">Upload a local file to the directory</span></span>
<span data-ttu-id="16e66-126">Teraz przekażemy plik lokalny do katalogu.</span><span class="sxs-lookup"><span data-stu-id="16e66-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="16e66-127">W poniższym przykładzie plik zostanie przekazany z lokalizacji `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="16e66-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="16e66-128">Zmień ścieżkę pliku tak, aby wskazywała prawidłowy plik na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="16e66-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="16e66-129">Wyświetlanie listy plików w katalogu</span><span class="sxs-lookup"><span data-stu-id="16e66-129">List the files in the directory</span></span>
<span data-ttu-id="16e66-130">Aby zobaczyć plik w katalogu, możesz wyświetlić listę wszystkich plików w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="16e66-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="16e66-131">To polecenie zwraca pliki i podkatalogi (jeśli istnieją) w katalogu CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="16e66-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="16e66-132">Polecenie Get-AzureStorageFile zwraca listę plików i katalogów dla dowolnego przekazanego obiektu katalogu.</span><span class="sxs-lookup"><span data-stu-id="16e66-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="16e66-133">Polecenie „Get-AzureStorageFile -Share $s” zwraca listę plików i katalogów w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="16e66-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="16e66-134">Aby uzyskać listę plików w podkatalogu, trzeba przekazać nazwę podkatalogu do polecenia Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="16e66-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="16e66-135">Tak właśnie działa powyższy zapis — pierwsza część polecenia do kreski pionowej zwraca wystąpienie katalogu dla podkatalogu CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="16e66-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="16e66-136">Następnie jest ono przekazywane do polecenia Get-AzureStorageFile, które zwraca pliki i katalogi w podkatalogu CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="16e66-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="16e66-137">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="16e66-137">Copy files</span></span>
<span data-ttu-id="16e66-138">Począwszy od wersji 0.9.7 programu Azure PowerShell, można kopiować pliki do innych plików, pliki do obiektów blob oraz obiekty blob do plików.</span><span class="sxs-lookup"><span data-stu-id="16e66-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="16e66-139">Poniżej przedstawiamy sposób wykonywania tych operacji kopiowania za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16e66-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="16e66-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16e66-140">Next steps</span></span>
<span data-ttu-id="16e66-141">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="16e66-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="16e66-142">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="16e66-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="16e66-143">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="16e66-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)