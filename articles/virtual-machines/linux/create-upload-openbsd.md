---
title: Tworzenie i przekazywanie obrazu OpenBSD maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tworzenie i przekazywanie wirtualnego dysku twardego (VHD) z systemem operacyjnym OpenBSD, aby utworzyć maszynę wirtualną platformy Azure za pomocą wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 716c07f6a738189d6cf2b3caafa16b753927d182
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-to-azure"></a><span data-ttu-id="de16b-103">Tworzenie i przekazywanie obrazu dysku OpenBSD na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="de16b-103">Create and Upload an OpenBSD disk image to Azure</span></span>
<span data-ttu-id="de16b-104">W tym artykule opisano tworzenie i przekazywanie wirtualnego dysku twardego (VHD) z systemem operacyjnym OpenBSD.</span><span class="sxs-lookup"><span data-stu-id="de16b-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the OpenBSD operating system.</span></span> <span data-ttu-id="de16b-105">Po wysłaniu, służy ona jako własnego obrazu można utworzyć maszynę wirtualną (VM) na platformie Azure za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de16b-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="de16b-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="de16b-106">Prerequisites</span></span>
<span data-ttu-id="de16b-107">W tym artykule przyjęto założenie, że masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="de16b-107">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="de16b-108">**Subskrypcja platformy Azure** — Jeśli nie masz konta, możesz utworzyć jedną w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="de16b-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="de16b-109">Jeśli masz subskrypcję MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="de16b-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="de16b-110">W przeciwnym razie Dowiedz się, jak [utworzyć bezpłatne konto próbne](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de16b-110">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="de16b-111">**Azure CLI 2.0** — upewnij się, że masz najnowszą [Azure CLI 2.0](/cli/azure/install-azure-cli) zainstalowane i zalogowany do konta platformy Azure z [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="de16b-111">**Azure CLI 2.0** - Make sure you have the latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in to your Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="de16b-112">**OpenBSD zainstalowanego systemu operacyjnego w pliku VHD** -obsługiwany system operacyjny OpenBSD (w wersji 6.1) musi być zainstalowana w wirtualnym dysku twardym.</span><span class="sxs-lookup"><span data-stu-id="de16b-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed to a virtual hard disk.</span></span> <span data-ttu-id="de16b-113">Istnieje wiele narzędzi do tworzenia plików VHD.</span><span class="sxs-lookup"><span data-stu-id="de16b-113">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="de16b-114">Na przykład umożliwia rozwiązanie wirtualizacji, takich jak funkcja Hyper-V Utwórz plik VHD i zainstalowania systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="de16b-114">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="de16b-115">Aby uzyskać instrukcje dotyczące instalowania i używania funkcji Hyper-V, zobacz [Instalowanie funkcji Hyper-V i tworzenie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="de16b-115">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="de16b-116">Przygotowywanie obrazu OpenBSD dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de16b-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="de16b-117">Na maszynie Wirtualnej, w którym zainstalowano system operacyjny OpenBSD 6.1, dodanego funkcji Hyper-V obsługi, wykonaj następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="de16b-117">On the VM where you installed the OpenBSD operating system 6.1, which added Hyper-V support, complete the following procedures:</span></span>

1. <span data-ttu-id="de16b-118">Jeśli podczas instalacji nie jest włączony protokół DHCP, włącz usługę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-118">If DHCP is not enabled during installation, enable the service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="de16b-119">Konfigurowanie konsoli szeregowej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="de16b-120">Instalacja pakietu należy skonfigurować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="de16b-121">Domyślnie `root` użytkownik jest wyłączony na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de16b-121">By default, the `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="de16b-122">Użytkownicy mogą uruchamiać polecenia z podwyższonym poziomem uprawnień przy użyciu `doas` na OpenBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de16b-122">Users can run commands with elevated privileges by using the `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="de16b-123">Doas jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="de16b-123">Doas is enabled by default.</span></span> <span data-ttu-id="de16b-124">Aby uzyskać więcej informacji, zobacz [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="de16b-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="de16b-125">Zainstaluj i skonfiguruj wymagania wstępne dotyczące agenta platformy Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-125">Install and configure prerequisites for the Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="de16b-126">Najnowszą wersję agenta programu Azure zawsze można znaleźć w [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="de16b-126">The latest release of the Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="de16b-127">Zainstaluj agenta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-127">Install the agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="de16b-128">Po zainstalowaniu agenta platformy Azure jest dobrym pomysłem jest sprawdzenie, czy działa w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-128">After you install Azure Agent, it's a good idea to verify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="de16b-129">Anulowanie zastrzeżenia systemu do czyszczenia go i była odpowiednia dla reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="de16b-129">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="de16b-130">Następujące polecenie spowoduje również usunięcie ostatnie konto użytkownika elastycznie i skojarzone dane:</span><span class="sxs-lookup"><span data-stu-id="de16b-130">The following command also deletes the last provisioned user account and the associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="de16b-131">Teraz można zamknąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de16b-131">Now you can shut down your VM.</span></span>


## <a name="prepare-the-vhd"></a><span data-ttu-id="de16b-132">Przygotowywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="de16b-132">Prepare the VHD</span></span>
<span data-ttu-id="de16b-133">VHDX format jest nieobsługiwane w systemie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="de16b-133">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="de16b-134">Można konwertować na dysk stały format wirtualnego dysku twardego za pomocą Menedżera funkcji Hyper-V lub programu Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="de16b-134">You can convert the disk to fixed VHD format using Hyper-V Manager or the Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="de16b-135">Przykładem jest następujące.</span><span class="sxs-lookup"><span data-stu-id="de16b-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="de16b-136">Utwórz zasoby magazynu i przekaż</span><span class="sxs-lookup"><span data-stu-id="de16b-136">Create storage resources and upload</span></span>
<span data-ttu-id="de16b-137">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="de16b-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="de16b-138">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="de16b-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="de16b-139">Aby przekazać dysk VHD, Utwórz konto magazynu z [Tworzenie konta magazynu az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="de16b-139">To upload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="de16b-140">Nazwy konta magazynu musi być unikatowa, więc podać własną nazwę.</span><span class="sxs-lookup"><span data-stu-id="de16b-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="de16b-141">Poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu*:</span><span class="sxs-lookup"><span data-stu-id="de16b-141">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="de16b-142">Aby kontrolować dostęp do konta magazynu, należy uzyskać klucza magazynu z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-142">To control access to the storage account, obtain the storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="de16b-143">Aby rozdzielić logicznie możesz przekazać pliki VHD, należy utworzyć kontener w ramach konta magazynu z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="de16b-143">To logically separate the VHDs you upload, create a container within the storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="de16b-144">Na koniec, Przekaż dysk VHD o [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="de16b-145">Tworzenie maszyny Wirtualnej z dysk VHD</span><span class="sxs-lookup"><span data-stu-id="de16b-145">Create VM from your VHD</span></span>
<span data-ttu-id="de16b-146">Można utworzyć maszyny Wirtualnej z [przykładowy skrypt](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) lub bezpośrednio z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="de16b-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="de16b-147">Aby określić OpenBSD wirtualnego dysku twardego, należy przekazać, użyj `--image` parametru w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-147">To specify the OpenBSD VHD you uploaded, use the `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="de16b-148">Uzyskaj adres IP dla maszyny Wirtualnej z OpenBSD [az vm--adresy ip](/cli/azure/vm#list-ip-addresses) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="de16b-148">Obtain the IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="de16b-149">Teraz możesz SSH do maszyny Wirtualnej OpenBSD normal:</span><span class="sxs-lookup"><span data-stu-id="de16b-149">Now you can SSH to your OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="de16b-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de16b-150">Next steps</span></span>
<span data-ttu-id="de16b-151">Jeśli chcesz dowiedzieć się więcej na temat obsługi funkcji Hyper-V na OpenBSD6.1 odczytu [OpenBSD 6.1](https://www.openbsd.org/61.html) i [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="de16b-151">If you want to know more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="de16b-152">Jeśli chcesz utworzyć Maszynę wirtualną od dysków zarządzanych w odczytu [dysku az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="de16b-152">If you want to create a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 