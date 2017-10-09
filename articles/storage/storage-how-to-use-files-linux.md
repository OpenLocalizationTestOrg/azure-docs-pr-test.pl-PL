---
title: "Magazyn plików Azure z systemem Linux aaaUse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak udostępnić toomount plików Azure za pośrednictwem protokołu SMB w systemie Linux."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="65cd8-103">Użyj usługi Magazyn plików Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="65cd8-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="65cd8-104">[Magazyn plików Azure](storage-dotnet-how-to-use-files.md) jest system plików w chmurze łatwe toouse firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="65cd8-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="65cd8-105">Udziały plików platformy Azure można zainstalować w dystrybucje systemu Linux przy użyciu hello [pakietu cifs witryny](https://wiki.samba.org/index.php/LinuxCIFS_utils) z hello [projektu Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="65cd8-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="65cd8-106">W tym artykule opisano dwa sposoby toomount udziału plików platformy Azure: na żądanie z hello `mount` polecenia i na rozruchu, tworząc wpis w `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="65cd8-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="65cd8-107">W kolejności toomount udział plików Azure poza hello region platformy Azure, który jest obsługiwany, takich jak lokalnie lub w innym regionie Azure, hello systemu operacyjnego musi obsługiwać hello funkcji szyfrowania protokołu SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="65cd8-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="65cd8-108">Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra.</span><span class="sxs-lookup"><span data-stu-id="65cd8-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="65cd8-109">Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="65cd8-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="65cd8-110">W czasie hello publikowania ta funkcja została tooUbuntu backported z 16.04 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="65cd8-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="65cd8-111">Wymagania wstępne dla instalowanie udziału plików platformy Azure z systemem Linux i hello pakietem cifs witryny</span><span class="sxs-lookup"><span data-stu-id="65cd8-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="65cd8-112">**Wybierz dystrybucji systemu Linux, którą może mieć zainstalowany pakiet witryny cifs hello**: Firma Microsoft zaleca hello dystrybucje systemu Linux w galerii Azure obraz powitania po:</span><span class="sxs-lookup"><span data-stu-id="65cd8-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="65cd8-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="65cd8-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="65cd8-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="65cd8-114">RHEL 7+</span></span>
    * <span data-ttu-id="65cd8-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="65cd8-115">CentOS 7+</span></span>
    * <span data-ttu-id="65cd8-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="65cd8-116">Debian 8</span></span>
    * <span data-ttu-id="65cd8-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="65cd8-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="65cd8-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="65cd8-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="65cd8-119"><a id="install-cifs-utils"></a>**Witaj witryny cifs zainstalowano pakietu**: hello cifs witryny można zainstalować za pomocą Menedżera pakietów hello na dystrybucji systemu Linux hello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65cd8-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="65cd8-120">Na **Ubuntu** i **na podstawie Debian** dystrybucji, użyj hello `apt-get` Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="65cd8-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="65cd8-121">Na **RHEL** i **CentOS**, użyj hello `yum` Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="65cd8-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="65cd8-122">Na **openSUSE**, użyj hello `zypper` Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="65cd8-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="65cd8-123">W innych dystrybucji przy użyciu Menedżera odpowiedniego pakietu hello lub [Kompiluj ze źródła](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="65cd8-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="65cd8-124">**Podejmowanie decyzji o uprawnienia pliku lub katalogu hello hello zainstalowany udział**: W poniższych przykładach hello, używamy 0777, toogive odczytu, zapisu i wykonywania uprawnienia tooall użytkowników.</span><span class="sxs-lookup"><span data-stu-id="65cd8-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="65cd8-125">Można zastąpić go z innymi [uprawnienia chmod](https://en.wikipedia.org/wiki/Chmod) pożądane.</span><span class="sxs-lookup"><span data-stu-id="65cd8-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="65cd8-126">**Nazwa konta magazynu**: udział plików Azure toomount, muszą hello nazwy konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="65cd8-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="65cd8-127">**Klucz konta magazynu**: udział plików Azure toomount, będzie konieczne hello klucz podstawowy (lub dodatkowej) magazynu.</span><span class="sxs-lookup"><span data-stu-id="65cd8-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="65cd8-128">Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.</span><span class="sxs-lookup"><span data-stu-id="65cd8-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="65cd8-129">**Upewnij się, jest otwarty port 445**: SMB komunikuje się za pośrednictwem portu TCP 445 - Sprawdź toosee, czy Zapora nie blokuje TCP porty 445 z komputera klienta.</span><span class="sxs-lookup"><span data-stu-id="65cd8-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="65cd8-130">Zainstaluj hello na żądanie z udziału plików platformy Azure`mount`</span><span class="sxs-lookup"><span data-stu-id="65cd8-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="65cd8-131">**[Zainstalować hello cifs witryny pakietu dla dystrybucji systemu Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="65cd8-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="65cd8-132">**Utwórz folder na potrzeby punktu instalacji hello**: można to zrobić dowolne miejsce w systemie plików hello.</span><span class="sxs-lookup"><span data-stu-id="65cd8-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="65cd8-133">**Udział plików Azure hello toomount polecenia użyj hello instalacji**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` hello odpowiednie informacje.</span><span class="sxs-lookup"><span data-stu-id="65cd8-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="65cd8-134">Gdy wszystko będzie gotowe za pomocą hello udziału plików na platformę Azure, możesz użyć `sudo umount ./mymountpoint` toounmount hello udziału.</span><span class="sxs-lookup"><span data-stu-id="65cd8-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="65cd8-135">Tworzenie punktu instalacji trwałe hello udział plików Azure`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="65cd8-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="65cd8-136">**[Zainstalować hello cifs witryny pakietu dla dystrybucji systemu Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="65cd8-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="65cd8-137">**Utwórz folder na potrzeby punktu instalacji hello**: można to zrobić dowolne miejsce w systemie plików hello, ale należy toonote hello ścieżka bezwzględna hello folderu.</span><span class="sxs-lookup"><span data-stu-id="65cd8-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="65cd8-138">Witaj poniższy przykład tworzy folder w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="65cd8-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="65cd8-139">**Użyj hello następujące polecenie hello tooappend po wierszu zbyt`/etc/fstab`**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` hello odpowiednie informacje.</span><span class="sxs-lookup"><span data-stu-id="65cd8-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="65cd8-140">Można użyć `sudo mount -a` udział plików Azure hello toomount po edycji `/etc/fstab` zamiast ponownego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="65cd8-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="65cd8-141">Opinia</span><span class="sxs-lookup"><span data-stu-id="65cd8-141">Feedback</span></span>
<span data-ttu-id="65cd8-142">Użytkownicy systemu Linux, chcemy toohear od Ciebie!</span><span class="sxs-lookup"><span data-stu-id="65cd8-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="65cd8-143">Hello magazyn plików Azure do grupy użytkowników systemu Linux udostępnia forum dla Ciebie tooshare opinii ocenić i przyjęcie magazynu plików w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="65cd8-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="65cd8-144">Wiadomości e-mail [magazyn plików Azure użytkowników systemu Linux](mailto:azurefileslinuxusers@microsoft.com) grupy Użytkownicy hello toojoin.</span><span class="sxs-lookup"><span data-stu-id="65cd8-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65cd8-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65cd8-145">Next steps</span></span>
<span data-ttu-id="65cd8-146">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="65cd8-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="65cd8-147">Dokumentacja interfejsu API REST usługi plików</span><span class="sxs-lookup"><span data-stu-id="65cd8-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="65cd8-148">Przy użyciu programu Azure PowerShell z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="65cd8-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="65cd8-149">Jak toouse AzCopy z magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="65cd8-149">How toouse AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="65cd8-150">Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="65cd8-150">Using hello Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="65cd8-151">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="65cd8-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="65cd8-152">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="65cd8-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
