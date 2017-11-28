---
title: "Instalowanie udziału plików platformy Azure za pomocą protokołu SMB w systemie macOS | Microsoft Docs"
description: "Dowiedz się, jak zainstalować udział plików platformy Azure za pomocą protokołu SMB w systemie macOS."
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
ms.openlocfilehash: bc3d67745afb8bbffe7ec3462e995104daff9632
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="91af9-103">Instalowanie udziału plików platformy Azure za pomocą protokołu SMB w systemie macOS</span><span class="sxs-lookup"><span data-stu-id="91af9-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="91af9-104">[Azure File Storage](../storage-dotnet-how-to-use-files.md) to usługa firmy Microsoft umożliwiająca tworzenie i używanie udziałów plików sieciowych na platformie Azure zgodnie ze standardami branżowymi.</span><span class="sxs-lookup"><span data-stu-id="91af9-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="91af9-105">Udziały plików platformy Azure można instalować w systemach macOS Sierra (10.12) i El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="91af9-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="91af9-106">W tym artykule przedstawiono dwa różne sposoby instalowania udziału plików platformy Azure w systemie macOS — za pomocą interfejsu użytkownika programu Finder i Terminala.</span><span class="sxs-lookup"><span data-stu-id="91af9-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="91af9-107">Przed instalowaniem udziału plików platformy Azure przy użyciu protokołu SMB zaleca się wyłączenie podpisywanie pakietów SMB.</span><span class="sxs-lookup"><span data-stu-id="91af9-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="91af9-108">Niezastosowanie się do tego zalecenia może spowodować zmniejszenie wydajności podczas uzyskiwania dostępu do udziału plików platformy Azure z systemu macOS.</span><span class="sxs-lookup"><span data-stu-id="91af9-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="91af9-109">Połączenie SMB będzie szyfrowane, więc nie zostanie obniżone bezpieczeństwo Twojego połączenia.</span><span class="sxs-lookup"><span data-stu-id="91af9-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="91af9-110">Następujące polecenia wykonane z poziomu terminala spowodują wyłączenie podpisywania pakietów SMB, jak opisano w tym [artykule pomocy technicznej firmy Apple dotyczącym wyłączania podpisywania pakietów SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="91af9-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="91af9-111">Wymagania wstępne dotyczące instalowania udziału plików platformy Azure w systemie macOS</span><span class="sxs-lookup"><span data-stu-id="91af9-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="91af9-112">**Nazwa konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie podanie nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="91af9-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="91af9-113">**Klucz konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie posiadanie podstawowego (lub dodatkowego) klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="91af9-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="91af9-114">Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.</span><span class="sxs-lookup"><span data-stu-id="91af9-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="91af9-115">**Otwarty port 445**: Protokół SMB komunikuje się za pośrednictwem portu TCP 445.</span><span class="sxs-lookup"><span data-stu-id="91af9-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="91af9-116">Na komputerze klienckim (komputerze Mac) upewnij się, że zapora nie blokuje portu TCP 445.</span><span class="sxs-lookup"><span data-stu-id="91af9-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="91af9-117">Instalowanie udziału plików platformy Azure za pomocą programu Finder</span><span class="sxs-lookup"><span data-stu-id="91af9-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="91af9-118">**Otwórz program Finder**: Program Finder jest domyślnie otwarty w systemie macOS, ale możesz się upewnić, że jest on aktualnie wybraną aplikacją, klikając „ikonę twarzy systemu macOS” w Docku:</span><span class="sxs-lookup"><span data-stu-id="91af9-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="91af9-119">![Ikona twarzy systemu macOS](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="91af9-119">![The macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="91af9-120">**W menu „Idź” wybierz pozycję „Połącz z serwerem”**: W ścieżce UNC z [wymagań wstępnych](#preq) przekształć początkowy podwójny ukośnik odwrotny (`\\`) w ciąg `smb://`, a wszystkie pozostałe ukośniki odwrotne (`\`) w ukośniki (`/`).</span><span class="sxs-lookup"><span data-stu-id="91af9-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="91af9-121">Twój link powinien wyglądać podobnie do następującego: ![Okno dialogowe „Łączenie z serwerem”](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="91af9-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="91af9-122">**Użyj nazwy udziału i klucza konta magazynu w wyświetlonym monicie o podanie nazwy użytkownika i hasła**: Po kliknięciu przycisku „Połącz” w oknie dialogowym „Łączenie z serwerem” zostanie wyświetlony monit o podanie nazwy użytkownika i hasła (pole zostanie automatycznie wypełnione nazwą użytkownika systemu macOS).</span><span class="sxs-lookup"><span data-stu-id="91af9-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="91af9-123">Istnieje możliwość umieszczenia nazwy udziału / klucza konta magazynu w pęku kluczy systemu macOS.</span><span class="sxs-lookup"><span data-stu-id="91af9-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="91af9-124">**Użyj udziału plików platformy Azure zgodnie z potrzebami**: Udział zostanie zainstalowany po podstawieniu nazwy udziału oraz klucza konta magazynu w polach nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="91af9-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="91af9-125">Udziału można używać tak samo jak lokalnego folderu / udziału plików. Obsługiwane jest też przeciąganie i upuszczanie plików do udziału plików:</span><span class="sxs-lookup"><span data-stu-id="91af9-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Migawka przedstawiająca zainstalowany udział plików platformy Azure](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="91af9-127">Instalowanie udziału plików platformy Azure za pomocą Terminala</span><span class="sxs-lookup"><span data-stu-id="91af9-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="91af9-128">Zastąp wartość `<storage-account-name>` nazwą konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="91af9-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="91af9-129">Jeśli zostanie wyświetlony monit, podaj klucz konta magazynu jako hasło.</span><span class="sxs-lookup"><span data-stu-id="91af9-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="91af9-130">**Użyj udziału plików platformy Azure zgodnie z potrzebami**: Udział plików platformy Azure zostanie zainstalowany w punkcie instalacji określonym w poprzednim poleceniu.</span><span class="sxs-lookup"><span data-stu-id="91af9-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Migawka przedstawiająca zainstalowany udział plików platformy Azure](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="91af9-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91af9-132">Next steps</span></span>
<span data-ttu-id="91af9-133">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="91af9-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="91af9-134">Artykuł pomocy technicznej firmy Apple — Łączenie z funkcją Udostępnianie plików na komputerze Mac</span><span class="sxs-lookup"><span data-stu-id="91af9-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="91af9-135">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="91af9-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="91af9-136">Rozwiązywanie problemów w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="91af9-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="91af9-137">Rozwiązywanie problemów w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="91af9-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    