---
title: "udział plików Azure aaaMount za pośrednictwem protokołu SMB macOS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak udostępnić toomount plików Azure za pośrednictwem protokołu SMB z macOS."
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
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="2b78b-103">Instalowanie udziału plików platformy Azure za pomocą protokołu SMB w systemie macOS</span><span class="sxs-lookup"><span data-stu-id="2b78b-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="2b78b-104">[Magazyn plików Azure](../storage-dotnet-how-to-use-files.md) usługi firmy Microsoft, która umożliwia toocreate i użyj udziałów plików sieciowych w hello Azure używa hello branżowymi.</span><span class="sxs-lookup"><span data-stu-id="2b78b-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="2b78b-105">Udziały plików platformy Azure można instalować w systemach macOS Sierra (10.12) i El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="2b78b-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="2b78b-106">W tym artykule przedstawiono dwa różne sposoby toomount udziału plików platformy Azure na macOS z hello interfejsu użytkownika wyszukiwania i przy użyciu hello terminalu.</span><span class="sxs-lookup"><span data-stu-id="2b78b-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="2b78b-107">Przed instalowaniem udziału plików platformy Azure przy użyciu protokołu SMB zaleca się wyłączenie podpisywanie pakietów SMB.</span><span class="sxs-lookup"><span data-stu-id="2b78b-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="2b78b-108">Nie w ten sposób może spowodować niską wydajnością, dostęp do udziału plików platformy Azure hello macOS.</span><span class="sxs-lookup"><span data-stu-id="2b78b-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="2b78b-109">Połączenia SMB, będą szyfrowane, więc nie ma to wpływu na powitania zabezpieczeń połączenia.</span><span class="sxs-lookup"><span data-stu-id="2b78b-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="2b78b-110">Z terminala hello, hello następujące polecenia spowoduje wyłączenie podpisywanie pakietów, jak opisano to [artykuł pomocy technicznej firmy Apple po wyłączeniu podpisywanie pakietów](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="2b78b-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="2b78b-111">Wymagania wstępne dotyczące instalowania udziału plików platformy Azure w systemie macOS</span><span class="sxs-lookup"><span data-stu-id="2b78b-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="2b78b-112">**Nazwa konta magazynu**: udział plików Azure toomount, muszą hello nazwy konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="2b78b-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="2b78b-113">**Klucz konta magazynu**: udział plików Azure toomount, będzie konieczne hello klucz podstawowy (lub dodatkowej) magazynu.</span><span class="sxs-lookup"><span data-stu-id="2b78b-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="2b78b-114">Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.</span><span class="sxs-lookup"><span data-stu-id="2b78b-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="2b78b-115">**Otwarty port 445**: Protokół SMB komunikuje się za pośrednictwem portu TCP 445.</span><span class="sxs-lookup"><span data-stu-id="2b78b-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="2b78b-116">Na komputerze klienckim (hello Mac) sprawdź toomake się, że Zapora nie blokuje TCP port 445.</span><span class="sxs-lookup"><span data-stu-id="2b78b-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="2b78b-117">Instalowanie udziału plików platformy Azure za pomocą programu Finder</span><span class="sxs-lookup"><span data-stu-id="2b78b-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="2b78b-118">**Otwórz wyszukiwanie**: wyszukiwanie jest otwarty na macOS domyślnie, ale można zapewnić jest hello aktualnie zaznaczonej aplikacji, klikając hello "macOS stają przed ikonę" hello dokowania:</span><span class="sxs-lookup"><span data-stu-id="2b78b-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="2b78b-119">![System macOS Hello stają przed ikony](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="2b78b-119">![hello macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="2b78b-120">**Wybierz pozycję "Connect tooServer" z Menu "Idź" hello**: przy użyciu ścieżki UNC hello z hello [wymagania wstępne](#preq), przekonwertować hello początku podwójny ukośnik odwrotny (`\\`) zbyt`smb://` i wszystkie inne ukośników odwrotnych (`\`) tooforwards ukośniki (`/`).</span><span class="sxs-lookup"><span data-stu-id="2b78b-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="2b78b-121">Łącze powinien wyglądać jak poniżej hello: ![hello "Connect tooServer" w oknie dialogowym](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="2b78b-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="2b78b-122">**Użyj hello udziału nazwy i przechowywanie klucza konta po wyświetleniu monitu o nazwę użytkownika i hasło**: gdy na powitania "Connect tooServer" w oknie dialogowym kliknij przycisk "Połącz", zostanie wyświetlony monit o hello nazwę użytkownika i hasło (są to autopopulated z Twojej macOS Nazwa użytkownika).</span><span class="sxs-lookup"><span data-stu-id="2b78b-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="2b78b-123">Dostępna jest opcja hello umieszczenie klucz konta magazynowania nazwa udziału hello w Twojej macOS łańcucha kluczy.</span><span class="sxs-lookup"><span data-stu-id="2b78b-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="2b78b-124">**Użyj udziału plików platformy Azure hello zgodnie z potrzebami**: po podstawiając hello udziału nazwy i magazynu klucz konta w hello nazwy użytkownika i hasła, zostanie zainstalowany hello udziału.</span><span class="sxs-lookup"><span data-stu-id="2b78b-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="2b78b-125">Mogą wykorzystać te informacje, jak w przypadku normalnie udział pliku/folderu lokalnego, w tym przeciąganie i upuszczanie plików w udziale plików hello:</span><span class="sxs-lookup"><span data-stu-id="2b78b-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Migawka przedstawiająca zainstalowany udział plików platformy Azure](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="2b78b-127">Instalowanie udziału plików platformy Azure za pomocą Terminala</span><span class="sxs-lookup"><span data-stu-id="2b78b-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="2b78b-128">Zastąp `<storage-account-name>` hello nazwą konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2b78b-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="2b78b-129">Jeśli zostanie wyświetlony monit, podaj klucz konta magazynu jako hasło.</span><span class="sxs-lookup"><span data-stu-id="2b78b-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="2b78b-130">**Użyj udziału plików platformy Azure hello zgodnie z potrzebami**: hello udziału plików platformy Azure zostanie zainstalowany w punkcie instalacji hello określony przez hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="2b78b-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Migawka hello zainstalować udział plików Azure](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="2b78b-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b78b-132">Next steps</span></span>
<span data-ttu-id="2b78b-133">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="2b78b-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="2b78b-134">Artykuł pomocy technicznej firmy Apple - jak tooconnect z udostępnianie plików na komputerze Mac</span><span class="sxs-lookup"><span data-stu-id="2b78b-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="2b78b-135">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="2b78b-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="2b78b-136">Rozwiązywanie problemów w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="2b78b-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="2b78b-137">Rozwiązywanie problemów w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="2b78b-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    