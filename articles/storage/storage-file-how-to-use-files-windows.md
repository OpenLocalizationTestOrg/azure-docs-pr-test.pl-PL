---
title: "aaaMount udziału plików platformy Azure i hello dostępu do udziału w systemie Windows | Dokumentacja firmy Microsoft"
description: "Instalowanie udziału plików platformy Azure i udziału hello dostępu w systemie Windows."
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="c5f40-103">Instalowanie udziału plików platformy Azure i udziału hello dostępu w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="c5f40-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="c5f40-104">[Magazyn plików Azure](storage-dotnet-how-to-use-files.md) jest system plików w chmurze łatwe toouse firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c5f40-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="c5f40-105">Udziały plików platformy Azure można instalować w systemie Windows i Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c5f40-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="c5f40-106">W tym artykule przedstawiono trzy różne sposoby toomount udział plików Azure w systemie Windows: z hello Interfejsu Eksploratora plików, za pomocą programu PowerShell i za pośrednictwem hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c5f40-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="c5f40-107">W kolejności toomount udział plików Azure poza hello region platformy Azure, który jest obsługiwany w, takich jak lokalnie lub w innym regionie Azure hello systemu operacyjnego musi obsługiwać protokół SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="c5f40-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="c5f40-108">Udział plików platformy Azure można zainstalować na maszynie z systemem Windows w środowisku lokalnym lub na maszynie wirtualnej platformy Azure, w zależności od wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c5f40-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="c5f40-109">Poniższej tabeli przedstawiono hello</span><span class="sxs-lookup"><span data-stu-id="c5f40-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="c5f40-110">Wersja systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c5f40-110">Windows Version</span></span>        | <span data-ttu-id="c5f40-111">Wersja protokołu SMB</span><span class="sxs-lookup"><span data-stu-id="c5f40-111">SMB Version</span></span> |<span data-ttu-id="c5f40-112">Instalacja na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c5f40-112">Mountable On Azure VM</span></span>|<span data-ttu-id="c5f40-113">Instalacja w środowisku lokalnym</span><span class="sxs-lookup"><span data-stu-id="c5f40-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="c5f40-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c5f40-114">Windows 7</span></span>              | <span data-ttu-id="c5f40-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="c5f40-115">SMB 2.1</span></span>     | <span data-ttu-id="c5f40-116">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-116">Yes</span></span>                 | <span data-ttu-id="c5f40-117">Nie</span><span class="sxs-lookup"><span data-stu-id="c5f40-117">No</span></span>                  |
| <span data-ttu-id="c5f40-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c5f40-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="c5f40-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="c5f40-119">SMB 2.1</span></span>     | <span data-ttu-id="c5f40-120">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-120">Yes</span></span>                 | <span data-ttu-id="c5f40-121">Nie</span><span class="sxs-lookup"><span data-stu-id="c5f40-121">No</span></span>                  |
| <span data-ttu-id="c5f40-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="c5f40-122">Windows 8</span></span>              | <span data-ttu-id="c5f40-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="c5f40-123">SMB 3.0</span></span>     | <span data-ttu-id="c5f40-124">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-124">Yes</span></span>                 | <span data-ttu-id="c5f40-125">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-125">Yes</span></span>                 |
| <span data-ttu-id="c5f40-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c5f40-126">Windows Server 2012</span></span>    | <span data-ttu-id="c5f40-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="c5f40-127">SMB 3.0</span></span>     | <span data-ttu-id="c5f40-128">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-128">Yes</span></span>                 | <span data-ttu-id="c5f40-129">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-129">Yes</span></span>                 |
| <span data-ttu-id="c5f40-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c5f40-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="c5f40-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="c5f40-131">SMB 3.0</span></span>     | <span data-ttu-id="c5f40-132">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-132">Yes</span></span>                 | <span data-ttu-id="c5f40-133">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-133">Yes</span></span>                 |
| <span data-ttu-id="c5f40-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c5f40-134">Windows 10</span></span>             | <span data-ttu-id="c5f40-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="c5f40-135">SMB 3.0</span></span>     | <span data-ttu-id="c5f40-136">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-136">Yes</span></span>                 | <span data-ttu-id="c5f40-137">Tak</span><span class="sxs-lookup"><span data-stu-id="c5f40-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="c5f40-138">Zawsze zalecamy z argumentami hello KB najnowszej wersji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c5f40-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="c5f40-139"></a>Wymagania wstępne dotyczące instalowania udziału plików platformy Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="c5f40-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="c5f40-140">**Nazwa konta magazynu**: udział plików Azure toomount, muszą hello nazwy konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="c5f40-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="c5f40-141">**Klucz konta magazynu**: udział plików Azure toomount, będzie konieczne hello klucz podstawowy (lub dodatkowej) magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5f40-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="c5f40-142">Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.</span><span class="sxs-lookup"><span data-stu-id="c5f40-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="c5f40-143">**Otwarty port 445**: Usługa Azure File Storage korzysta z protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="c5f40-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="c5f40-144">SMB komunikuje się za pośrednictwem portu TCP 445 - Sprawdź toosee, czy Zapora nie blokuje porty TCP 445 z komputera klienta.</span><span class="sxs-lookup"><span data-stu-id="c5f40-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="c5f40-145">Instalowanie udziału plików Azure hello z Eksploratora plików</span><span class="sxs-lookup"><span data-stu-id="c5f40-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="c5f40-146">Należy pamiętać, że Witaj, postępując zgodnie z instrukcjami są wyświetlane w systemie Windows 10 i może różnić się nieznacznie w starszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="c5f40-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="c5f40-147">**Otwórz okno Eksploratora plików**: można to zrobić przez otwarcie z hello Start Menu lub naciskając klawisz skrótu Win + E.</span><span class="sxs-lookup"><span data-stu-id="c5f40-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="c5f40-148">**Przejdź element "Ten komputer" toohello na powitania po lewej stronie powitania okna. Spowoduje to zmianę menu hello hello Wstążce. W obszarze hello komputera menu, wybierz "Mapuj dysk sieciowy"**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Zrzut ekranu przedstawiający menu rozwijanego "Mapuj dysk sieciowy" hello](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="c5f40-150">**Ścieżka UNC hello kopiowania z okienka "Połącz" hello w portalu Azure hello**: szczegółowy opis sposobu toofind te informacje można znaleźć [tutaj](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="c5f40-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![ścieżka UNC Hello w okienku Połącz magazyn plików Azure hello](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="c5f40-152">**Wybierz hello literę dysku, a następnie wprowadź ścieżkę UNC hello.**</span><span class="sxs-lookup"><span data-stu-id="c5f40-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Zrzut ekranu okna dialogowego powitania "Mapuj dysk sieciowy"](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="c5f40-154">**Użyj hello nazwy konta magazynu poprzedzony przez `Azure\` jako hello nazwy użytkownika i klucz konta magazynu, jako hello hasła.**</span><span class="sxs-lookup"><span data-stu-id="c5f40-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Zrzut ekranu okna dialogowego poświadczeń sieciowych hello](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="c5f40-156">**Użyj udziału plików platformy Azure zgodnie z potrzebami**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-156">**Use Azure File share as desired**.</span></span>
    
    ![Udział plików platformy Azure jest teraz zainstalowany](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="c5f40-158">**Gdy są gotowe toodismount (lub odłączyć) hello udziału plików platformy Azure możesz to zrobić przez kliknięcie prawym przyciskiem myszy na zapis hello hello udziału w obszarze hello "lokalizacje sieciowe" w Eksploratorze plików i wybierając polecenie "Rozłącz"**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="c5f40-159">Instalowanie udziału plików Azure hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5f40-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="c5f40-160">**Użyj hello następujące polecenie udział plików Azure hello toomount**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello odpowiednie informacje.</span><span class="sxs-lookup"><span data-stu-id="c5f40-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="c5f40-161">**Użyj udziału plików platformy Azure hello zgodnie z potrzebami**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="c5f40-162">**Gdy skończysz, należy odinstalować hello udziału plików platformy Azure przy użyciu następującego polecenia hello**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="c5f40-163">Można użyć hello `-Persist` parametru `New-PSDrive` hello toomake pozostałe toohello widoczne udział plików Azure hello systemu operacyjnego, gdy jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c5f40-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="c5f40-164">Instalowanie udziału plików Azure hello z wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c5f40-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="c5f40-165">**Użyj hello następujące polecenie udział plików Azure hello toomount**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello odpowiednie informacje.</span><span class="sxs-lookup"><span data-stu-id="c5f40-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="c5f40-166">**Użyj udziału plików platformy Azure hello zgodnie z potrzebami**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="c5f40-167">**Gdy skończysz, należy odinstalować hello udziału plików platformy Azure przy użyciu następującego polecenia hello**.</span><span class="sxs-lookup"><span data-stu-id="c5f40-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="c5f40-168">Witaj ponownie tooautomatically udział plików Azure można skonfigurować na ponowne uruchomienie komputera przez utrwalanie poświadczeń hello w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="c5f40-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="c5f40-169">następujące polecenie Hello zostanie utrzymana hello poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="c5f40-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="c5f40-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5f40-170">Next steps</span></span>
<span data-ttu-id="c5f40-171">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="c5f40-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="c5f40-172">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="c5f40-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="c5f40-173">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c5f40-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="c5f40-174">Artykuły koncepcyjne i filmy</span><span class="sxs-lookup"><span data-stu-id="c5f40-174">Conceptual articles and videos</span></span>
* <span data-ttu-id="c5f40-175">[Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)</span><span class="sxs-lookup"><span data-stu-id="c5f40-175">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="c5f40-176">Jak toouse magazyn plików Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="c5f40-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="c5f40-177">Narzędzia dostępne dla usługi Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="c5f40-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="c5f40-178">Używanie programu Azure PowerShell z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c5f40-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="c5f40-179">Jak toouse AzCopy z usługi Magazyn Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c5f40-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="c5f40-180">Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c5f40-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="c5f40-181">Rozwiązywanie problemów z usługą Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="c5f40-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="c5f40-182">Wpisy na blogach</span><span class="sxs-lookup"><span data-stu-id="c5f40-182">Blog posts</span></span>
* <span data-ttu-id="c5f40-183">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)</span><span class="sxs-lookup"><span data-stu-id="c5f40-183">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)</span></span>
* <span data-ttu-id="c5f40-184">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="c5f40-184">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* <span data-ttu-id="c5f40-185">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="c5f40-185">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)</span></span>
* [<span data-ttu-id="c5f40-186">Migrowanie danych tooAzure pliku</span><span class="sxs-lookup"><span data-stu-id="c5f40-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="c5f40-187">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="c5f40-187">Reference</span></span>
* [<span data-ttu-id="c5f40-188">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="c5f40-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="c5f40-189">Dokumentacja interfejsu API REST usługi plików</span><span class="sxs-lookup"><span data-stu-id="c5f40-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
