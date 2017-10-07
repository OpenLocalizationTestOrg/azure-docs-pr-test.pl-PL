---
title: "aaaMount magazyn plików Azure na maszynach wirtualnych systemu Linux przy użyciu protokołu SMB 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak toomount magazyn plików Azure na maszynach wirtualnych systemu Linux przy użyciu protokołu SMB"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="0d637-103">Magazyn plików Azure instalacji na maszynach wirtualnych systemu Linux przy użyciu protokołu SMB 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d637-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="0d637-104">W tym artykule opisano, jak toomount magazyn plików Azure na maszynie Wirtualnej systemu Linux przy użyciu hello protokołu bloku komunikatów serwera (SMB).</span><span class="sxs-lookup"><span data-stu-id="0d637-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="0d637-105">Magazyn plików oferuje udziały plików w chmurze hello za pośrednictwem hello standardowego protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="0d637-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="0d637-106">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="0d637-106">hello requirements are:</span></span>

* <span data-ttu-id="0d637-107">[Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="0d637-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="0d637-108">Secure Shell (SSH) publicznego i prywatnego klucza plików</span><span class="sxs-lookup"><span data-stu-id="0d637-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="0d637-109">Toouse wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0d637-109">CLI versions toouse</span></span>
<span data-ttu-id="0d637-110">Hello zadanie można wykonać za pomocą jednego z hello następujące wersje interfejsu wiersza polecenia (CLI):</span><span class="sxs-lookup"><span data-stu-id="0d637-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="0d637-111">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="0d637-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0d637-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="0d637-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="0d637-113">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="0d637-113">Quick commands</span></span>
<span data-ttu-id="0d637-114">zadanie hello tooaccomplish szybkie, wykonaj kroki hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d637-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="0d637-115">Aby uzyskać szczegółowe informacje i kontekstu, rozpoczęcie hello ["Szczegółowy przewodnik"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d637-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0d637-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0d637-116">Prerequisites</span></span>
* <span data-ttu-id="0d637-117">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="0d637-117">A resource group</span></span>
* <span data-ttu-id="0d637-118">Sieć wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d637-118">An Azure virtual network</span></span>
* <span data-ttu-id="0d637-119">Grupa zabezpieczeń sieci przy użyciu protokołu SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="0d637-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="0d637-120">Podsieci</span><span class="sxs-lookup"><span data-stu-id="0d637-120">A subnet</span></span>
* <span data-ttu-id="0d637-121">Konto magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d637-121">An Azure storage account</span></span>
* <span data-ttu-id="0d637-122">Klucze konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d637-122">Azure storage account keys</span></span>
* <span data-ttu-id="0d637-123">Udział magazynu plików Azure</span><span class="sxs-lookup"><span data-stu-id="0d637-123">An Azure File storage share</span></span>
* <span data-ttu-id="0d637-124">Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0d637-124">A Linux VM</span></span>

<span data-ttu-id="0d637-125">Przykładami należy zastąpić własnymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="0d637-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="0d637-126">Utwórz katalog instalacji lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="0d637-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="0d637-127">Zainstaluj punkt instalacji toohello udziału SMB hello pliku magazynu</span><span class="sxs-lookup"><span data-stu-id="0d637-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="0d637-128">Utrwalanie hello instalacji po ponownym uruchomieniu</span><span class="sxs-lookup"><span data-stu-id="0d637-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="0d637-129">Dodaj powitania po wierszu zbyt`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="0d637-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0d637-130">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="0d637-130">Detailed walkthrough</span></span>

<span data-ttu-id="0d637-131">Magazyn plików oferuje udziały plików w chmurze hello używających standardowego protokołu SMB hello.</span><span class="sxs-lookup"><span data-stu-id="0d637-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="0d637-132">Witaj najnowszej wersji z pliku magazynu można również zainstalować udział plików z dowolnego systemu operacyjnego, który obsługuje protokół SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="0d637-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="0d637-133">Użycie instalacji SMB w systemie Linux, otrzymasz łatwe tworzenie kopii zapasowych tooa niezawodne, stała archiwizacji lokalizacji magazynu, która jest obsługiwana przez umowy dotyczącej poziomu usług.</span><span class="sxs-lookup"><span data-stu-id="0d637-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="0d637-134">Przenoszenie plików z instalacji SMB tooan maszyny Wirtualnej znajdującej się na magazyn plików jest toodebug doskonałym sposobem logowania.</span><span class="sxs-lookup"><span data-stu-id="0d637-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="0d637-135">Wynika to z faktu hello udziału SMB tego samego mogą być instalowane lokalnie tooyour Mac, Linux lub Windows stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="0d637-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="0d637-136">SMB nie jest najlepszym rozwiązaniem hello do przesyłania strumieniowego Linux lub dzienniki aplikacji w czasie rzeczywistym, ponieważ hello protokołu SMB nie jest skompilowany toohandle tych obowiązków duże rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="0d637-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="0d637-137">Narzędzia rejestrowania dedykowanych, ujednoliconej warstwy, takiego jak Fluentd będzie lepszym rozwiązaniem niż SMB zbierania systemu Linux i aplikacji, rejestrowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0d637-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="0d637-138">Aby to szczegółowe wskazówki utworzymy hello wymagania wstępne niezbędne toofirst utworzyć udział magazynu plików hello, a następnie zainstalować go za pośrednictwem protokołu SMB na maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0d637-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="0d637-139">Utwórz konto magazynu platformy Azure przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="0d637-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="0d637-140">Pokaż klucze konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0d637-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="0d637-141">Podczas tworzenia konta magazynu, klucze konta hello są tworzone w parach, dzięki czemu można obracać bez przerw w działaniu usługi.</span><span class="sxs-lookup"><span data-stu-id="0d637-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="0d637-142">Po przełączeniu toohello drugi klucz w parze hello, możesz utworzyć nową parę kluczy.</span><span class="sxs-lookup"><span data-stu-id="0d637-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="0d637-143">Nowe klucze konta magazynu zawsze są tworzone w parach, sprawdzając, czy zawsze jest co najmniej jeden nieużywane magazynu kluczy gotowe tooswitch do.</span><span class="sxs-lookup"><span data-stu-id="0d637-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="0d637-144">tooshow hello klucze konta magazynu, należy użyć hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="0d637-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="0d637-145">Utwórz udział magazynu plików hello.</span><span class="sxs-lookup"><span data-stu-id="0d637-145">Create hello File storage share.</span></span>

    <span data-ttu-id="0d637-146">udział magazynu plików Hello zawiera hello udziału SMB.</span><span class="sxs-lookup"><span data-stu-id="0d637-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="0d637-147">przydział Hello jest zawsze wyrażona w gigabajtów (GB).</span><span class="sxs-lookup"><span data-stu-id="0d637-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="0d637-148">toocreate hello udział magazynu plików, użyj następującego kodu hello:</span><span class="sxs-lookup"><span data-stu-id="0d637-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="0d637-149">Utwórz katalog punktu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="0d637-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="0d637-150">Należy utworzyć w hello Linux pliku system toomount hello udziału SMB do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0d637-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="0d637-151">Cokolwiek zapisu lub odczytu z katalogu instalacji lokalnej hello są przesyłane dalej toohello udziału SMB, który znajduje się w pliku magazynu.</span><span class="sxs-lookup"><span data-stu-id="0d637-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="0d637-152">toocreate hello katalog hello Użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="0d637-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="0d637-153">Zainstaluj hello udziału SMB przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="0d637-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="0d637-154">Utrwalanie hello SMB instalacji podczas ponownych rozruchów.</span><span class="sxs-lookup"><span data-stu-id="0d637-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="0d637-155">Po ponownym uruchomieniu maszyny Wirtualnej systemu Linux hello hello zainstalowany udział SMB jest odinstalowane podczas zamykania.</span><span class="sxs-lookup"><span data-stu-id="0d637-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="0d637-156">tooremount hello udziale SMB podczas rozruchu, należy dodać toohello wiersza /etc/fstab systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0d637-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="0d637-157">Linux używa hello fstab pliku toolist hello systemów plików wymaga toomount, podczas procesu rozruchu hello.</span><span class="sxs-lookup"><span data-stu-id="0d637-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="0d637-158">Dodawanie udziału SMB hello gwarantuje, że ten udział magazynu plików hello jest trwale zainstalowany system plików dla hello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0d637-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="0d637-159">Dodawanie hello pliku magazynu SMB udziału tooa nowej maszyny Wirtualnej jest możliwe, gdy używasz init chmury.</span><span class="sxs-lookup"><span data-stu-id="0d637-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="0d637-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d637-160">Next steps</span></span>

- [<span data-ttu-id="0d637-161">Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0d637-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="0d637-162">Dodaj tooa dysku maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0d637-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="0d637-163">Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d637-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
