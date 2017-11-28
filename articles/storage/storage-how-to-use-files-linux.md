---
title: "Magazyn plików Azure za pomocą systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować udział plików Azure za pośrednictwem protokołu SMB w systemie Linux."
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
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="b1484-103">Użyj usługi Magazyn plików Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="b1484-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="b1484-104">[Azure File Storage](storage-dotnet-how-to-use-files.md) to łatwy w użyciu system plików w chmurze firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b1484-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="b1484-105">Udziały plików platformy Azure można zainstalować w dystrybucje systemu Linux przy użyciu [pakietu cifs witryny](https://wiki.samba.org/index.php/LinuxCIFS_utils) z [projektu Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="b1484-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="b1484-106">W tym artykule przedstawiono dwie metody, aby zainstalować udział plików Azure: na żądanie z `mount` polecenia i na rozruchu, tworząc wpis w `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="b1484-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="b1484-107">Aby zainstalować udział plików Azure poza Azure region, który jest obsługiwany, takich jak lokalnie lub w innym regionie Azure, system operacyjny musi obsługiwać funkcje szyfrowania protokołu SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="b1484-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="b1484-108">Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra.</span><span class="sxs-lookup"><span data-stu-id="b1484-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="b1484-109">Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="b1484-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="b1484-110">Podczas publikowania ta funkcja została backported do Ubuntu z 16.04 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="b1484-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="b1484-111">Konfigurator służący do instalowania plików Azure udostępniać Linux oraz pakiet cifs witryny</span><span class="sxs-lookup"><span data-stu-id="b1484-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="b1484-112">**Wybierz dystrybucji systemu Linux, który może mieć zainstalowanym pakietem cifs witryny**: Firma Microsoft zaleca następujące dystrybucje systemu Linux w galerii Azure obrazu:</span><span class="sxs-lookup"><span data-stu-id="b1484-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="b1484-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="b1484-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="b1484-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="b1484-114">RHEL 7+</span></span>
    * <span data-ttu-id="b1484-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="b1484-115">CentOS 7+</span></span>
    * <span data-ttu-id="b1484-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="b1484-116">Debian 8</span></span>
    * <span data-ttu-id="b1484-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="b1484-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="b1484-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="b1484-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="b1484-119"><a id="install-cifs-utils"></a>**Zainstalowano pakiet cifs witryny**: witryny cifs można zainstalować za pomocą Menedżera pakietu na dystrybucji systemu Linux wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b1484-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="b1484-120">Na **Ubuntu** i **na podstawie Debian** dystrybucji, użyj `apt-get` Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="b1484-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="b1484-121">Na **RHEL** i **CentOS**, użyj `yum` Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="b1484-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="b1484-122">Na **openSUSE**, użyj `zypper` Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="b1484-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="b1484-123">W innych dystrybucji przy użyciu Menedżera odpowiedniego pakietu lub [Kompiluj ze źródła](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="b1484-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="b1484-124">**Podejmowanie decyzji o uprawnienia pliku lub katalogu zainstalowany udział**: W poniższym przykładzie używamy 0777, aby dać odczytu, zapisu i wykonywania uprawnienia do wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b1484-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="b1484-125">Można zastąpić go z innymi [uprawnienia chmod](https://en.wikipedia.org/wiki/Chmod) pożądane.</span><span class="sxs-lookup"><span data-stu-id="b1484-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="b1484-126">**Nazwa konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie podanie nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1484-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="b1484-127">**Klucz konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie posiadanie podstawowego (lub dodatkowego) klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1484-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="b1484-128">Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.</span><span class="sxs-lookup"><span data-stu-id="b1484-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="b1484-129">**Upewnij się, jest otwarty port 445**: SMB komunikuje się za pośrednictwem portu TCP 445 — Sprawdź, czy Zapora nie blokuje TCP, porty 445 z komputera klienta.</span><span class="sxs-lookup"><span data-stu-id="b1484-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="b1484-130">Instalacji plików Azure udostępniania na żądanie za pomocą`mount`</span><span class="sxs-lookup"><span data-stu-id="b1484-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="b1484-131">**[Zainstaluj pakiet cifs witryny dla dystrybucji systemu Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="b1484-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="b1484-132">**Utwórz folder na potrzeby punktu instalacji**: można to zrobić dowolne miejsce w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="b1484-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="b1484-133">**Aby zainstalować udział plików Azure za pomocą polecenia instalacji**: Pamiętaj, aby zastąpić `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` przy użyciu odpowiednich informacji.</span><span class="sxs-lookup"><span data-stu-id="b1484-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="b1484-134">Po zakończeniu korzystania z udziału plików platformy Azure, możesz użyć `sudo umount ./mymountpoint` odinstalował udziału.</span><span class="sxs-lookup"><span data-stu-id="b1484-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="b1484-135">Utwórz punkt trwałej dla udziału plików platformy Azure z`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="b1484-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="b1484-136">**[Zainstaluj pakiet cifs witryny dla dystrybucji systemu Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="b1484-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="b1484-137">**Utwórz folder na potrzeby punktu instalacji**: można to zrobić dowolne miejsce w systemie plików, ale należy pamiętać, bezwzględną ścieżkę do folderu.</span><span class="sxs-lookup"><span data-stu-id="b1484-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="b1484-138">Poniższy przykład tworzy folder w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="b1484-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="b1484-139">**Użyj następującego polecenia, aby dołączyć następujący wiersz do `/etc/fstab`** : Pamiętaj, aby zastąpić `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` przy użyciu odpowiednich informacji.</span><span class="sxs-lookup"><span data-stu-id="b1484-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="b1484-140">Można użyć `sudo mount -a` Aby zainstalować udział plików Azure po zakończeniu edycji `/etc/fstab` zamiast ponownego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="b1484-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="b1484-141">Opinia</span><span class="sxs-lookup"><span data-stu-id="b1484-141">Feedback</span></span>
<span data-ttu-id="b1484-142">Użytkownicy systemu Linux, chcemy poznać Twoją opinię!</span><span class="sxs-lookup"><span data-stu-id="b1484-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="b1484-143">Magazyn plików Azure dla grupy Użytkownicy systemu Linux udostępnia forum można udostępnić opinii, oceny i przyjęcie magazynu plików w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="b1484-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="b1484-144">Wiadomości e-mail [magazyn plików Azure użytkowników systemu Linux](mailto:azurefileslinuxusers@microsoft.com) dołączenia do grupy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b1484-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1484-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1484-145">Next steps</span></span>
<span data-ttu-id="b1484-146">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="b1484-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="b1484-147">Dokumentacja interfejsu API REST usługi plików</span><span class="sxs-lookup"><span data-stu-id="b1484-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="b1484-148">Przy użyciu programu Azure PowerShell z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="b1484-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="b1484-149">Jak używać narzędzia AzCopy z magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b1484-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="b1484-150">Przy użyciu wiersza polecenia platformy Azure z usługą Azure storage</span><span class="sxs-lookup"><span data-stu-id="b1484-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="b1484-151">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b1484-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="b1484-152">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="b1484-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
