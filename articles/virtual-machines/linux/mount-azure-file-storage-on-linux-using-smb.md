---
title: "Magazyn plików Azure na maszynach wirtualnych systemu Linux za pomocą protokołu SMB aaaMount | Dokumentacja firmy Microsoft"
description: "Jak toomount na maszynach wirtualnych systemu Linux za pomocą protokołu SMB z usługi Magazyn plików Azure hello Azure CLI 2.0"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="7147b-103">Magazyn plików Azure instalacji na maszynach wirtualnych systemu Linux za pomocą protokołu SMB</span><span class="sxs-lookup"><span data-stu-id="7147b-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="7147b-104">W tym artykule opisano, jak zainstalować hello tooutilize Usługa Magazyn plików Azure na maszynie Wirtualnej systemu Linux za pomocą protokołu SMB z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7147b-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="7147b-105">Magazyn plików Azure oferuje udziały plików w chmurze hello przy użyciu standardowego protokołu SMB hello.</span><span class="sxs-lookup"><span data-stu-id="7147b-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="7147b-106">Można również wykonać te kroki hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7147b-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7147b-107">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="7147b-107">hello requirements are:</span></span>

- [<span data-ttu-id="7147b-108">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7147b-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="7147b-109">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="7147b-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="7147b-110">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="7147b-110">Quick Commands</span></span>

* <span data-ttu-id="7147b-111">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="7147b-111">A resource group</span></span>
* <span data-ttu-id="7147b-112">Sieć wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7147b-112">An Azure virtual network</span></span>
* <span data-ttu-id="7147b-113">Grupa zabezpieczeń sieci przy użyciu protokołu SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="7147b-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="7147b-114">Podsieci</span><span class="sxs-lookup"><span data-stu-id="7147b-114">A subnet</span></span>
* <span data-ttu-id="7147b-115">Konto magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7147b-115">An Azure storage account</span></span>
* <span data-ttu-id="7147b-116">Klucze konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7147b-116">Azure storage account keys</span></span>
* <span data-ttu-id="7147b-117">Udział magazynu plików Azure</span><span class="sxs-lookup"><span data-stu-id="7147b-117">An Azure File storage share</span></span>
* <span data-ttu-id="7147b-118">Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7147b-118">A Linux VM</span></span>

<span data-ttu-id="7147b-119">Przykładami należy zastąpić własnymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="7147b-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="7147b-120">Utwórz katalog instalacji lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="7147b-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="7147b-121">Zainstaluj punkt instalacji toohello udziału SMB hello pliku magazynu</span><span class="sxs-lookup"><span data-stu-id="7147b-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="7147b-122">Utrwalanie hello instalacji po ponownym uruchomieniu</span><span class="sxs-lookup"><span data-stu-id="7147b-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="7147b-123">toodo tak, Dodaj powitania po wierszu toohello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="7147b-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="7147b-124">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="7147b-124">Detailed walkthrough</span></span>

<span data-ttu-id="7147b-125">Magazyn plików oferuje udziały plików w chmurze hello używających standardowego protokołu SMB hello.</span><span class="sxs-lookup"><span data-stu-id="7147b-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="7147b-126">Witaj najnowszej wersji z pliku magazynu można również zainstalować udział plików z dowolnego systemu operacyjnego, który obsługuje protokół SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="7147b-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="7147b-127">Użycie instalacji SMB w systemie Linux, otrzymasz łatwe tworzenie kopii zapasowych tooa niezawodne, stała archiwizacji lokalizacji magazynu, która jest obsługiwana przez umowy dotyczącej poziomu usług.</span><span class="sxs-lookup"><span data-stu-id="7147b-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="7147b-128">Przenoszenie plików z instalacji SMB tooan maszyny Wirtualnej znajdującej się na magazyn plików jest toodebug doskonałym sposobem logowania.</span><span class="sxs-lookup"><span data-stu-id="7147b-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="7147b-129">Wynika to z faktu hello udziału SMB tego samego mogą być instalowane lokalnie tooyour Mac, Linux lub Windows stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="7147b-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="7147b-130">SMB nie jest najlepszym rozwiązaniem hello do przesyłania strumieniowego Linux lub dzienniki aplikacji w czasie rzeczywistym, ponieważ hello protokołu SMB nie jest skompilowany toohandle tych obowiązków duże rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="7147b-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="7147b-131">Narzędzia rejestrowania dedykowanych, ujednoliconej warstwy, takiego jak Fluentd będzie lepszym rozwiązaniem niż SMB zbierania systemu Linux i aplikacji, rejestrowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7147b-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="7147b-132">Aby to szczegółowe wskazówki utworzymy hello wymagania wstępne niezbędne toofirst utworzyć udział magazynu plików hello, a następnie zainstalować go za pośrednictwem protokołu SMB na maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7147b-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="7147b-133">Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create) udziału plików hello toohold.</span><span class="sxs-lookup"><span data-stu-id="7147b-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="7147b-134">Grupa zasobów o nazwie toocreate `myResourceGroup` w lokalizacji "Zachodnie stany USA" hello, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7147b-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="7147b-135">Utwórz konto magazynu platformy Azure z [Tworzenie konta magazynu az](/cli/azure/storage/account#create) toostore hello rzeczywistymi plikami.</span><span class="sxs-lookup"><span data-stu-id="7147b-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="7147b-136">toocreate konto magazynu o nazwie mojekontomagazynu przy użyciu magazynu Standard_LRS hello jednostka SKU, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7147b-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="7147b-137">Pokaż klucze konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="7147b-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="7147b-138">Podczas tworzenia konta magazynu, klucze konta hello są tworzone w parach, dzięki czemu można obracać bez przerw w działaniu usługi.</span><span class="sxs-lookup"><span data-stu-id="7147b-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="7147b-139">Po przełączeniu toohello drugi klucz w parze hello, możesz utworzyć nową parę kluczy.</span><span class="sxs-lookup"><span data-stu-id="7147b-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="7147b-140">Nowe klucze konta magazynu zawsze są tworzone w parach, sprawdzając, czy zawsze jest co najmniej jeden magazyn nieużywane konta klucza gotowe tooswitch do.</span><span class="sxs-lookup"><span data-stu-id="7147b-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="7147b-141">Wyświetl klucze konta magazynu hello hello [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="7147b-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="7147b-142">Witaj klucze konta magazynu dla hello o nazwie `mystorageaccount` są wymienione w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7147b-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="7147b-143">tooextract jednego klucza, użyj hello `--query` flagi.</span><span class="sxs-lookup"><span data-stu-id="7147b-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="7147b-144">Witaj poniższy przykład wyodrębnia hello pierwszego klucza (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="7147b-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="7147b-145">Utwórz udział magazynu plików hello.</span><span class="sxs-lookup"><span data-stu-id="7147b-145">Create hello File storage share.</span></span>

    <span data-ttu-id="7147b-146">udział magazynu plików Hello zawiera hello udziału SMB z [utworzyć udział magazynu az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="7147b-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="7147b-147">przydział Hello jest zawsze wyrażona w gigabajtów (GB).</span><span class="sxs-lookup"><span data-stu-id="7147b-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="7147b-148">Podaj jeden z kluczy hello z poprzednim hello `az storage account keys list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="7147b-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="7147b-149">Utwórz udział o nazwie mystorageshare z przydziału 10 GB, za pomocą hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7147b-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="7147b-150">Utwórz katalog punktu instalacji.</span><span class="sxs-lookup"><span data-stu-id="7147b-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="7147b-151">Utwórz katalog lokalny w hello Linux pliku system toomount hello do udziału SMB.</span><span class="sxs-lookup"><span data-stu-id="7147b-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="7147b-152">Cokolwiek zapisu lub odczytu z katalogu instalacji lokalnej hello są przesyłane dalej toohello udziału SMB, który znajduje się w pliku magazynu.</span><span class="sxs-lookup"><span data-stu-id="7147b-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="7147b-153">toocreate katalogu lokalnego na/mnt/mymountdirectory, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7147b-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="7147b-154">Zainstaluj katalogu lokalnego udziału toohello hello SMB.</span><span class="sxs-lookup"><span data-stu-id="7147b-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="7147b-155">Podaj własne nazwy użytkownika konta magazynu i klucza konta magazynu dla poświadczenia instalacji hello:</span><span class="sxs-lookup"><span data-stu-id="7147b-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="7147b-156">Utrwalanie hello SMB instalacji podczas ponownych rozruchów.</span><span class="sxs-lookup"><span data-stu-id="7147b-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="7147b-157">Po ponownym uruchomieniu maszyny Wirtualnej systemu Linux hello hello zainstalowany udział SMB jest odinstalowane podczas zamykania.</span><span class="sxs-lookup"><span data-stu-id="7147b-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="7147b-158">hello tooremount udziale SMB podczas rozruchu, Dodaj wiersz toohello /etc/fstab systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7147b-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="7147b-159">Linux używa hello fstab pliku toolist hello systemów plików wymaga toomount, podczas procesu rozruchu hello.</span><span class="sxs-lookup"><span data-stu-id="7147b-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="7147b-160">Dodawanie udziału SMB hello gwarantuje, że ten udział magazynu plików hello jest trwale zainstalowany system plików dla hello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7147b-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="7147b-161">Dodawanie hello pliku magazynu SMB udziału tooa nowej maszyny Wirtualnej jest możliwe, gdy używasz init chmury.</span><span class="sxs-lookup"><span data-stu-id="7147b-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="7147b-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7147b-162">Next steps</span></span>

- [<span data-ttu-id="7147b-163">Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7147b-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="7147b-164">Dodaj tooa dysku maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7147b-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="7147b-165">Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7147b-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
