---
title: "Instalowanie udziału plików platformy Azure i uzyskiwanie dostępu do udziału w systemie Windows | Microsoft Docs"
description: "Zainstaluj udział plików platformy Azure i uzyskaj dostępu do tego udziału w systemie Windows."
services: storage
documentationcenter: na
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
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="7e404-103">Instalowanie udziału plików platformy Azure i uzyskiwanie dostępu do udziału w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="7e404-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="7e404-104">[Azure File Storage](storage-dotnet-how-to-use-files.md) to łatwy w użyciu system plików w chmurze firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e404-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="7e404-105">Udziały plików platformy Azure można instalować w systemie Windows i Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7e404-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="7e404-106">W tym artykule przedstawiono trzy różne sposoby instalowania udziału plików platformy Azure w systemie Windows: za pomocą interfejsu użytkownika Eksploratora plików, programu PowerShell oraz wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7e404-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="7e404-107">Aby móc zainstalować udział plików platformy Azure poza regionem świadczenia usługi Azure, w którym jest on hostowany, na przykład lokalnie lub w innym regionie świadczenia usługi Azure, system operacyjny musi obsługiwać protokół SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="7e404-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="7e404-108">Udział plików platformy Azure można zainstalować na maszynie z systemem Windows w środowisku lokalnym lub na maszynie wirtualnej platformy Azure, w zależności od wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7e404-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="7e404-109">W poniższej tabeli przedstawiono</span><span class="sxs-lookup"><span data-stu-id="7e404-109">Below table illustrates the</span></span> 

| <span data-ttu-id="7e404-110">Wersja systemu Windows</span><span class="sxs-lookup"><span data-stu-id="7e404-110">Windows Version</span></span>        | <span data-ttu-id="7e404-111">Wersja protokołu SMB</span><span class="sxs-lookup"><span data-stu-id="7e404-111">SMB Version</span></span> |<span data-ttu-id="7e404-112">Instalacja na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7e404-112">Mountable On Azure VM</span></span>|<span data-ttu-id="7e404-113">Instalacja w środowisku lokalnym</span><span class="sxs-lookup"><span data-stu-id="7e404-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="7e404-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="7e404-114">Windows 7</span></span>              | <span data-ttu-id="7e404-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="7e404-115">SMB 2.1</span></span>     | <span data-ttu-id="7e404-116">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-116">Yes</span></span>                 | <span data-ttu-id="7e404-117">Nie</span><span class="sxs-lookup"><span data-stu-id="7e404-117">No</span></span>                  |
| <span data-ttu-id="7e404-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7e404-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="7e404-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="7e404-119">SMB 2.1</span></span>     | <span data-ttu-id="7e404-120">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-120">Yes</span></span>                 | <span data-ttu-id="7e404-121">Nie</span><span class="sxs-lookup"><span data-stu-id="7e404-121">No</span></span>                  |
| <span data-ttu-id="7e404-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="7e404-122">Windows 8</span></span>              | <span data-ttu-id="7e404-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="7e404-123">SMB 3.0</span></span>     | <span data-ttu-id="7e404-124">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-124">Yes</span></span>                 | <span data-ttu-id="7e404-125">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-125">Yes</span></span>                 |
| <span data-ttu-id="7e404-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7e404-126">Windows Server 2012</span></span>    | <span data-ttu-id="7e404-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="7e404-127">SMB 3.0</span></span>     | <span data-ttu-id="7e404-128">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-128">Yes</span></span>                 | <span data-ttu-id="7e404-129">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-129">Yes</span></span>                 |
| <span data-ttu-id="7e404-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7e404-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="7e404-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="7e404-131">SMB 3.0</span></span>     | <span data-ttu-id="7e404-132">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-132">Yes</span></span>                 | <span data-ttu-id="7e404-133">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-133">Yes</span></span>                 |
| <span data-ttu-id="7e404-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="7e404-134">Windows 10</span></span>             | <span data-ttu-id="7e404-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="7e404-135">SMB 3.0</span></span>     | <span data-ttu-id="7e404-136">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-136">Yes</span></span>                 | <span data-ttu-id="7e404-137">Tak</span><span class="sxs-lookup"><span data-stu-id="7e404-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="7e404-138">Zawsze zalecamy pobranie najnowszej aktualizacji KB dla danej wersji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="7e404-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="7e404-139"></a>Wymagania wstępne dotyczące instalowania udziału plików platformy Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="7e404-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="7e404-140">**Nazwa konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie podanie nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e404-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="7e404-141">**Klucz konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie posiadanie podstawowego (lub dodatkowego) klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e404-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="7e404-142">Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.</span><span class="sxs-lookup"><span data-stu-id="7e404-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="7e404-143">**Otwarty port 445**: Usługa Azure File Storage korzysta z protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="7e404-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="7e404-144">Protokół SMB komunikuje się za pośrednictwem portu TCP 445. Upewnij się, że Twoja zapora nie blokuje portów TCP 445 z komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="7e404-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="7e404-145">Instalowanie udziału plików platformy Azure za pomocą Eksploratora plików</span><span class="sxs-lookup"><span data-stu-id="7e404-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="7e404-146">Należy pamiętać, że następujące instrukcje dotyczą systemu Windows 10 i mogą być nieco inne w starszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="7e404-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="7e404-147">**Otwórz Eksploratora plików**: Można to zrobić przy użyciu menu Start lub przez naciśnięcie skrótu Win+E.</span><span class="sxs-lookup"><span data-stu-id="7e404-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="7e404-148">**Przejdź do elementu „Ten komputer” w lewej części okna. Spowoduje to zmianę menu dostępnego na wstążce. W menu Komputer wybierz pozycję „Mapuj dysk sieciowy”**.</span><span class="sxs-lookup"><span data-stu-id="7e404-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Zrzut ekranu przedstawiający menu rozwijane „Mapuj dysk sieciowy”](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="7e404-150">**Skopiuj ścieżkę UNC z okienka „Połącz” w witrynie Azure Portal**: szczegółowy opis znajdywania tych informacji można znaleźć [tutaj](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="7e404-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Ścieżka UNC z okienka Połącz usługi Azure File Storage](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="7e404-152">**Wybierz literę dysku i wprowadź ścieżkę UNC.**</span><span class="sxs-lookup"><span data-stu-id="7e404-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![Zrzut ekranu przedstawiający okno dialogowe „Mapowanie dysku sieciowego”](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="7e404-154">**Jako nazwy użytkownika użyj nazwy konta magazynu poprzedzonej ciągiem `Azure\`, a jako hasła użyj klucza konta magazynu.**</span><span class="sxs-lookup"><span data-stu-id="7e404-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![Zrzut ekranu okna dialogowego poświadczeń sieciowych](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="7e404-156">**Użyj udziału plików platformy Azure zgodnie z potrzebami**.</span><span class="sxs-lookup"><span data-stu-id="7e404-156">**Use Azure File share as desired**.</span></span>
    
    ![Udział plików platformy Azure jest teraz zainstalowany](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="7e404-158">**Gdy zajdzie potrzeba odinstalowania (lub odłączenia) udziału plików platformy Azure, możesz to zrobić przez kliknięcie prawym przyciskiem myszy wpisu dla udziału w obszarze „Lokalizacje sieciowe” w Eksploratorze plików i wybranie polecenia „Odłącz”**.</span><span class="sxs-lookup"><span data-stu-id="7e404-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="7e404-159">Instalowanie udziału plików platformy Azure za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e404-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="7e404-160">**Użyj następującego polecenia, aby zainstalować udział plików platformy Azure**: Pamiętaj, aby zastąpić ciągi `<storage-account-name>`, `<share-name>`, `<storage-account-key>` i `<desired-drive-letter>` odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="7e404-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="7e404-161">**Użyj udziału plików platformy Azure zgodnie z potrzebami**.</span><span class="sxs-lookup"><span data-stu-id="7e404-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="7e404-162">**Gdy skończysz, odinstaluj udział plików platformy Azure przy użyciu następującego polecenia**.</span><span class="sxs-lookup"><span data-stu-id="7e404-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="7e404-163">Możesz użyć parametru `-Persist` dla dysku `New-PSDrive`, aby po zainstalowaniu udział plików platformy Azure był widoczny dla reszty systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7e404-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="7e404-164">Instalowanie udziału plików platformy Azure za pomocą wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7e404-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="7e404-165">**Użyj następującego polecenia, aby zainstalować udział plików platformy Azure**: Pamiętaj, aby zastąpić ciągi `<storage-account-name>`, `<share-name>`, `<storage-account-key>` i `<desired-drive-letter>` odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="7e404-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="7e404-166">**Użyj udziału plików platformy Azure zgodnie z potrzebami**.</span><span class="sxs-lookup"><span data-stu-id="7e404-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="7e404-167">**Gdy skończysz, odinstaluj udział plików platformy Azure przy użyciu następującego polecenia**.</span><span class="sxs-lookup"><span data-stu-id="7e404-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="7e404-168">Poświadczenia dla udziału plików platformy Azure można przechowywać w systemie Windows, dzięki czemu udział może być automatycznie instalowany podczas ponownego uruchamiania komputera.</span><span class="sxs-lookup"><span data-stu-id="7e404-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="7e404-169">Następujące polecenie spowoduje utrwalenie poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="7e404-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="7e404-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e404-170">Next steps</span></span>
<span data-ttu-id="7e404-171">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="7e404-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="7e404-172">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="7e404-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="7e404-173">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="7e404-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="7e404-174">Artykuły koncepcyjne i filmy</span><span class="sxs-lookup"><span data-stu-id="7e404-174">Conceptual articles and videos</span></span>
* <span data-ttu-id="7e404-175">[Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)</span><span class="sxs-lookup"><span data-stu-id="7e404-175">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="7e404-176">Jak używać usługi Azure File Storage z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="7e404-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="7e404-177">Narzędzia dostępne dla usługi Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="7e404-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="7e404-178">Używanie programu Azure PowerShell z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7e404-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* <span data-ttu-id="7e404-179">[How to use AzCopy with Microsoft Azure Storage](storage-use-azcopy.md) (Jak używać narzędzia AzCopy z usługą Microsoft Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="7e404-179">[How to use AzCopy with Microsoft Azure Storage](storage-use-azcopy.md)</span></span>
* [<span data-ttu-id="7e404-180">Używanie interfejsu wiersza polecenia platformy Azure z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7e404-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="7e404-181">Rozwiązywanie problemów z usługą Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="7e404-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="7e404-182">Wpisy na blogach</span><span class="sxs-lookup"><span data-stu-id="7e404-182">Blog posts</span></span>
* <span data-ttu-id="7e404-183">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)</span><span class="sxs-lookup"><span data-stu-id="7e404-183">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)</span></span>
* <span data-ttu-id="7e404-184">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="7e404-184">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* <span data-ttu-id="7e404-185">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="7e404-185">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)</span></span>
* [<span data-ttu-id="7e404-186">Migrowanie danych do usługi Pliki Azure</span><span class="sxs-lookup"><span data-stu-id="7e404-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="7e404-187">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="7e404-187">Reference</span></span>
* [<span data-ttu-id="7e404-188">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="7e404-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="7e404-189">Dokumentacja interfejsu API REST usługi plików</span><span class="sxs-lookup"><span data-stu-id="7e404-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
