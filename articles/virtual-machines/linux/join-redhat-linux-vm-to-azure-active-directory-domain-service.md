---
title: "Dołącz RedHat Linux maszyny Wirtualnej do usług Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak sprzęgać istniejącej RedHat Enterprise Linux 7 maszyny Wirtualnej z platformy Azure usług domenowych Active Directory."
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
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: 2e46a0f3c9bdbe267d121b4bf62e25d5d411fcc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a><span data-ttu-id="c319b-103">Dołącz RedHat Linux maszyny Wirtualnej z usługą domeny usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c319b-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span></span>

<span data-ttu-id="c319b-104">W tym artykule przedstawiono sposób Dołącz maszynę wirtualną Red Hat Enterprise Linux (RHEL) 7 do domeny zarządzanej interfejsów Azure Active Directory domeny usług (AADDS).</span><span class="sxs-lookup"><span data-stu-id="c319b-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="c319b-105">Wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="c319b-105">The requirements are:</span></span>

- [<span data-ttu-id="c319b-106">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c319b-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="c319b-107">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="c319b-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="c319b-108">Azure Active Directory Domain Services kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="c319b-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="c319b-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="c319b-109">Quick Commands</span></span>

<span data-ttu-id="c319b-110">_Przykładami należy zastąpić własnymi ustawieniami._</span><span class="sxs-lookup"><span data-stu-id="c319b-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a><span data-ttu-id="c319b-111">Przełącznik wiersza polecenia platformy azure do trybu klasycznego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c319b-111">Switch the azure-cli to classic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="c319b-112">Wyszukaj RHEL wersji i obrazów</span><span class="sxs-lookup"><span data-stu-id="c319b-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="c319b-113">Utwórz Redhat Linux VM</span><span class="sxs-lookup"><span data-stu-id="c319b-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-to-the-vm"></a><span data-ttu-id="c319b-114">Łączenie przez protokół SSH z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="c319b-114">SSH to the VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="c319b-115">YUM pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="c319b-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="c319b-116">Zainstaluj wymagane pakiety</span><span class="sxs-lookup"><span data-stu-id="c319b-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="c319b-117">Teraz, wymagane pakiety są zainstalowane na maszynie wirtualnej systemu Linux, następne zadanie to można dołączyć maszyny wirtualnej do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="c319b-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

### <a name="discover-the-aad-domain-services-managed-domain"></a><span data-ttu-id="c319b-118">Odnajdywanie domeny zarządzanej usług domenowych w usłudze AAD</span><span class="sxs-lookup"><span data-stu-id="c319b-118">Discover the AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="c319b-119">Inicjowanie protokołu kerberos</span><span class="sxs-lookup"><span data-stu-id="c319b-119">Initialize kerberos</span></span>

<span data-ttu-id="c319b-120">Upewnij się, że określ użytkownika, który należy do grupy "Administratorzy kontrolera domeny usługi AAD".</span><span class="sxs-lookup"><span data-stu-id="c319b-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="c319b-121">Tylko ci użytkownicy mogą dołączania komputerów do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="c319b-121">Only these users can join computers to the managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a><span data-ttu-id="c319b-122">Dołącz maszynę do domeny</span><span class="sxs-lookup"><span data-stu-id="c319b-122">Join the machine to the domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a><span data-ttu-id="c319b-123">Sprawdź, czy komputer jest przyłączony do domeny</span><span class="sxs-lookup"><span data-stu-id="c319b-123">Verify the machine is joined to the domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="c319b-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c319b-124">Next Steps</span></span>

* [<span data-ttu-id="c319b-125">Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c319b-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c319b-126">Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c319b-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c319b-127">Wdrażanie i zarządzanie maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c319b-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
