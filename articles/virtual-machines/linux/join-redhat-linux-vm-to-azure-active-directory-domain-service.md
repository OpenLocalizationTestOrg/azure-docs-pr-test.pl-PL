---
title: aaaJoin tooan maszyny Wirtualnej systemu Linux RedHat Azure Active Directory DS | Dokumentacja firmy Microsoft
description: "Jak toojoin tooan istniejącej maszyny Wirtualnej z RedHat Enterprise Linux 7 usługi Azure Active Directory domeny."
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
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="e9884-103">Dołącz do maszyny Wirtualnej systemu Linux RedHat tooan usług domenowych Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9884-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="e9884-104">W tym artykule opisano sposób toojoin tooan maszyny wirtualnej Red Hat Enterprise Linux (RHEL) 7 interfejsów Azure Active Directory domeny usług (AADDS) zarządzania domeny.</span><span class="sxs-lookup"><span data-stu-id="e9884-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="e9884-105">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="e9884-105">hello requirements are:</span></span>

- [<span data-ttu-id="e9884-106">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e9884-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="e9884-107">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="e9884-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="e9884-108">Azure Active Directory Domain Services kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="e9884-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="e9884-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="e9884-109">Quick Commands</span></span>

<span data-ttu-id="e9884-110">_Przykładami należy zastąpić własnymi ustawieniami._</span><span class="sxs-lookup"><span data-stu-id="e9884-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="e9884-111">Przełącznik wiersza polecenia platformy azure hello tooclassic wdrożeń w trybie</span><span class="sxs-lookup"><span data-stu-id="e9884-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="e9884-112">Wyszukaj RHEL wersji i obrazów</span><span class="sxs-lookup"><span data-stu-id="e9884-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="e9884-113">Utwórz Redhat Linux VM</span><span class="sxs-lookup"><span data-stu-id="e9884-113">Create a Redhat Linux VM</span></span>

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

### <a name="ssh-toohello-vm"></a><span data-ttu-id="e9884-114">Toohello SSH maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e9884-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="e9884-115">YUM pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="e9884-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="e9884-116">Zainstaluj wymagane pakiety</span><span class="sxs-lookup"><span data-stu-id="e9884-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="e9884-117">Obecnie pakiety hello wymagane są zainstalowane na maszynie wirtualnej systemu Linux hello, następne zadanie hello jest domeny zarządzanej toohello toojoin hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e9884-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="e9884-118">Odnajdywanie domeny zarządzanej usług domenowych w usłudze AAD hello</span><span class="sxs-lookup"><span data-stu-id="e9884-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="e9884-119">Inicjowanie protokołu kerberos</span><span class="sxs-lookup"><span data-stu-id="e9884-119">Initialize kerberos</span></span>

<span data-ttu-id="e9884-120">Upewnij się, że podajesz użytkownik, który należy toohello "AAD kontrolera domeny" Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="e9884-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="e9884-121">Tylko ci użytkownicy można przyłączyć do domeny zarządzanej toohello komputerów.</span><span class="sxs-lookup"><span data-stu-id="e9884-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="e9884-122">Dołącz do domeny toohello maszyny hello</span><span class="sxs-lookup"><span data-stu-id="e9884-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="e9884-123">Sprawdź, czy komputer hello jest toohello przyłączone do domeny</span><span class="sxs-lookup"><span data-stu-id="e9884-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="e9884-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9884-124">Next Steps</span></span>

* [<span data-ttu-id="e9884-125">Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e9884-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e9884-126">Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e9884-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e9884-127">Wdrażanie i zarządzanie maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e9884-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
