---
title: "aaaHow toouse PowerShell toomanage magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toouse toomanage środowiska PowerShell usługi Magazyn plików Azure."
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
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="b01a7-103">Jak toouse toomanage środowiska PowerShell usługi Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="b01a7-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="b01a7-104">Można użyć programu Azure PowerShell toocreate i Zarządzanie udziałami plików.</span><span class="sxs-lookup"><span data-stu-id="b01a7-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="b01a7-105">Zainstaluj hello poleceń cmdlet programu PowerShell dla usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b01a7-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="b01a7-106">toouse tooprepare programu PowerShell, Pobierz i zainstaluj polecenia cmdlet programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b01a7-107">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) hello zainstalować instrukcje instalacji i punktu.</span><span class="sxs-lookup"><span data-stu-id="b01a7-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="b01a7-108">Zaleca się pobrać i zainstalować lub uaktualnić toohello najnowsze modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b01a7-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="b01a7-109">Otwórz okno programu Azure PowerShell, klikając przycisk **Start** i wpisując polecenie **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b01a7-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="b01a7-110">okno programu PowerShell Hello obliczeniowymi hello modułu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="b01a7-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="b01a7-111">Tworzenie kontekstu konta magazynu i klucza</span><span class="sxs-lookup"><span data-stu-id="b01a7-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="b01a7-112">Tworzenie kontekstu konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-112">Create hello storage account context.</span></span> <span data-ttu-id="b01a7-113">kontekst Hello hermetyzuje hello magazynu konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="b01a7-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="b01a7-114">Aby uzyskać instrukcje dotyczące kopiowania klucza konta z hello [portalu Azure](https://portal.azure.com), zobacz [wyświetlanie i kopiowanie kluczy dostępu do magazynu](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="b01a7-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="b01a7-115">Zastąp `storage-account-name` i `storage-account-key` z nazwy konta magazynu i klucza w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="b01a7-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="b01a7-116">Tworzenie nowego udziału plików</span><span class="sxs-lookup"><span data-stu-id="b01a7-116">Create a new file share</span></span>
<span data-ttu-id="b01a7-117">Utwórz nowy udział hello, o nazwie `logs`.</span><span class="sxs-lookup"><span data-stu-id="b01a7-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="b01a7-118">Masz już udział plików w usłudze Magazyn plików.</span><span class="sxs-lookup"><span data-stu-id="b01a7-118">You now have a file share in File storage.</span></span> <span data-ttu-id="b01a7-119">Teraz dodamy katalog i plik.</span><span class="sxs-lookup"><span data-stu-id="b01a7-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b01a7-120">Witaj nazwa udziału plików musi być tylko małe litery.</span><span class="sxs-lookup"><span data-stu-id="b01a7-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="b01a7-121">Szczegółowe informacje o nazwach plików i udziałów plików można znaleźć w temacie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Nazywanie i odwoływanie się do udziałów, katalogów, plików i metadanych).</span><span class="sxs-lookup"><span data-stu-id="b01a7-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="b01a7-122">Tworzenie katalogu w udziale plików hello</span><span class="sxs-lookup"><span data-stu-id="b01a7-122">Create a directory in hello file share</span></span>
<span data-ttu-id="b01a7-123">Tworzenie katalogu w udziale hello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-123">Create a directory in hello share.</span></span> <span data-ttu-id="b01a7-124">W hello poniższy przykład, nosi nazwę katalogu hello `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="b01a7-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="b01a7-125">Przekazywanie pliku lokalnego katalogu toohello</span><span class="sxs-lookup"><span data-stu-id="b01a7-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="b01a7-126">Teraz można przekazać pliku lokalnego katalogu toohello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="b01a7-127">Witaj poniższym przykładzie plik zostanie przekazany z `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="b01a7-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="b01a7-128">Edytuj hello ścieżkę pliku tak, aby wskazywało tooa prawidłowy plik na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b01a7-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="b01a7-129">Lista plików hello hello katalogu</span><span class="sxs-lookup"><span data-stu-id="b01a7-129">List hello files in hello directory</span></span>
<span data-ttu-id="b01a7-130">toosee hello pliku w katalogu hello, możesz wyświetlić listę wszystkich plików z katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="b01a7-131">To polecenie zwraca hello pliki i podkatalogi (jeśli istnieją) w katalogu CustomLogs hello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="b01a7-132">Polecenie Get-AzureStorageFile zwraca listę plików i katalogów dla dowolnego przekazanego obiektu katalogu.</span><span class="sxs-lookup"><span data-stu-id="b01a7-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="b01a7-133">"Polecenia get-AzureStorageFile-Share $s" zwraca listę plików i katalogów w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="b01a7-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="b01a7-134">tooget listę plików w podkatalogu, masz hello toopass tooGet polecenia podkatalogu-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="b01a7-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="b01a7-135">Jest to czego — pierwsza część polecenia hello zapasowej potoku toohello hello Zwraca wystąpienie katalogu hello podkatalogu CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="b01a7-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="b01a7-136">Następnie jest ono przekazywane do polecenia Get-AzureStorageFile, która zwraca hello pliki i katalogi w podkatalogu CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="b01a7-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="b01a7-137">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="b01a7-137">Copy files</span></span>
<span data-ttu-id="b01a7-138">Począwszy od wersji 0.9.7 programu Azure PowerShell, można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b01a7-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="b01a7-139">Poniżej przedstawiamy, jak tooperform je skopiować operacji za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b01a7-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="b01a7-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b01a7-140">Next steps</span></span>
<span data-ttu-id="b01a7-141">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="b01a7-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="b01a7-142">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b01a7-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="b01a7-143">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="b01a7-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)