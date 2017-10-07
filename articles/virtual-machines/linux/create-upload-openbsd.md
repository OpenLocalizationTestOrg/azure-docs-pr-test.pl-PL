---
title: aaaCreate i przekazywanie wirtualna OpenBSD obrazu tooAzure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello OpenBSD toocreate systemu operacyjnego maszyny wirtualnej platformy Azure za pomocą wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="da8db-103">Tworzenie i przekazywanie tooAzure obrazu dysku OpenBSD</span><span class="sxs-lookup"><span data-stu-id="da8db-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="da8db-104">W tym artykule opisano, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello OpenBSD systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da8db-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="da8db-105">Po wysłaniu, można użyć jej jako toocreate własny obraz maszyny wirtualnej (VM) na platformie Azure za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da8db-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="da8db-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="da8db-106">Prerequisites</span></span>
<span data-ttu-id="da8db-107">W tym artykule założono, że hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="da8db-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="da8db-108">**Subskrypcja platformy Azure** — Jeśli nie masz konta, możesz utworzyć jedną w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="da8db-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="da8db-109">Jeśli masz subskrypcję MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="da8db-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="da8db-110">W przeciwnym razie Dowiedz się, jak za[utworzyć bezpłatne konto próbne](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da8db-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="da8db-111">**Azure CLI 2.0** — upewnij się, że masz hello najnowszych [Azure CLI 2.0](/cli/azure/install-azure-cli) zainstalowane i zarejestrowane w tooyour konto platformy Azure z [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="da8db-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="da8db-112">**OpenBSD zainstalowanego systemu operacyjnego w pliku VHD** -obsługiwany system operacyjny OpenBSD (w wersji 6.1) musi być zainstalowany tooa wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="da8db-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="da8db-113">Wiele narzędzi istnieje toocreate pliki VHD.</span><span class="sxs-lookup"><span data-stu-id="da8db-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="da8db-114">Można na przykład, takich jak plik VHD hello toocreate funkcji Hyper-V za pomocą rozwiązania wirtualizacji i zainstaluj system operacyjny hello.</span><span class="sxs-lookup"><span data-stu-id="da8db-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="da8db-115">Aby uzyskać instrukcje dotyczące sposobu tooinstall i użyj funkcji Hyper-V, zobacz [Instalowanie funkcji Hyper-V i tworzenie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="da8db-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="da8db-116">Przygotowywanie obrazu OpenBSD dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="da8db-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="da8db-117">Na powitania maszyny Wirtualnej, w którym zainstalowano hello OpenBSD systemie operacyjnym 6.1, w którym dodano obsługę funkcji Hyper-V, wykonaj hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="da8db-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="da8db-118">Jeśli protokół DHCP nie jest włączony podczas instalacji, włącz usługę hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="da8db-119">Konfigurowanie konsoli szeregowej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="da8db-120">Instalacja pakietu należy skonfigurować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="da8db-121">Domyślnie program hello `root` użytkownik jest wyłączony na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da8db-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="da8db-122">Użytkownicy mogą uruchamiać polecenia z podwyższonym poziomem uprawnień przy użyciu hello `doas` na OpenBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da8db-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="da8db-123">Doas jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="da8db-123">Doas is enabled by default.</span></span> <span data-ttu-id="da8db-124">Aby uzyskać więcej informacji, zobacz [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="da8db-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="da8db-125">Zainstaluj i skonfiguruj wymagania wstępne dotyczące hello Azure agenta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="da8db-126">najnowszą wersję Hello hello Azure agenta zawsze można znaleźć w [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="da8db-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="da8db-127">Zainstaluj agenta hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="da8db-128">Po zainstalowaniu agenta platformy Azure jest tooverify dobrym rozwiązaniem, która działa w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="da8db-129">Deprovision hello tooclean systemu go i udostępnić go odpowiednie dla reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="da8db-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="da8db-130">Witaj następujące polecenie spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie i hello skojarzone dane:</span><span class="sxs-lookup"><span data-stu-id="da8db-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="da8db-131">Teraz można zamknąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da8db-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="da8db-132">Przygotowanie hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="da8db-132">Prepare hello VHD</span></span>
<span data-ttu-id="da8db-133">Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="da8db-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="da8db-134">Możesz przekonwertować hello dysku toofixed formatu wirtualnego dysku twardego za pomocą Menedżera funkcji Hyper-V lub hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="da8db-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="da8db-135">Przykładem jest następujące.</span><span class="sxs-lookup"><span data-stu-id="da8db-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="da8db-136">Utwórz zasoby magazynu i przekaż</span><span class="sxs-lookup"><span data-stu-id="da8db-136">Create storage resources and upload</span></span>
<span data-ttu-id="da8db-137">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="da8db-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="da8db-138">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="da8db-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="da8db-139">tooupload dysk VHD, Utwórz konto magazynu z [Tworzenie konta magazynu az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="da8db-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="da8db-140">Nazwy konta magazynu musi być unikatowa, więc podać własną nazwę.</span><span class="sxs-lookup"><span data-stu-id="da8db-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="da8db-141">Witaj poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu*:</span><span class="sxs-lookup"><span data-stu-id="da8db-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="da8db-142">toocontrol uzyskać dostęp do konta magazynu toohello, uzyskać klucza magazynu hello z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="da8db-143">oddzielne hello toologically wirtualne dyski twarde można przekazać utworzyć kontener w ramach konta magazynu hello z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="da8db-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="da8db-144">Na koniec, Przekaż dysk VHD o [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="da8db-145">Tworzenie maszyny Wirtualnej z dysk VHD</span><span class="sxs-lookup"><span data-stu-id="da8db-145">Create VM from your VHD</span></span>
<span data-ttu-id="da8db-146">Można utworzyć maszyny Wirtualnej z [przykładowy skrypt](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) lub bezpośrednio z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="da8db-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="da8db-147">toospecify hello OpenBSD wirtualnego dysku twardego został przekazany, użyj hello `--image` parametru w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="da8db-148">Uzyskaj adres IP powitania dla maszyny Wirtualnej z OpenBSD [az vm--adresy ip](/cli/azure/vm#list-ip-addresses) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da8db-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="da8db-149">Teraz można tooyour SSH maszyny Wirtualnej OpenBSD normal:</span><span class="sxs-lookup"><span data-stu-id="da8db-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="da8db-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da8db-150">Next steps</span></span>
<span data-ttu-id="da8db-151">Więcej informacji na temat funkcji Hyper-V obsługuje na OpenBSD6.1 tooknow należy odczytać [OpenBSD 6.1](https://www.openbsd.org/61.html) i [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="da8db-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="da8db-152">Chcąc toocreate Maszynę wirtualną od dysków zarządzanych, przeczytaj [dysku az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="da8db-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
