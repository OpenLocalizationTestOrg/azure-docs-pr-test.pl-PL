---
title: "aaaAzure Windows przykłady interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykłady systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="bb6e2-103">Maszyny wirtualne platformy Azure CLI przykłady dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bb6e2-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="bb6e2-104">Witaj Poniższa tabela zawiera łącza toobash skrypty utworzone przy użyciu interfejsu wiersza polecenia Azure hello wdrażanie maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="bb6e2-105">**Tworzenie maszyn wirtualnych**</span><span class="sxs-lookup"><span data-stu-id="bb6e2-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="bb6e2-106">Utwórz maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="bb6e2-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-107">Tworzy maszynę wirtualną systemu Windows z minimalną konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="bb6e2-108">Utwórz maszynę wirtualną w pełni skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="bb6e2-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-109">Tworzy grupę zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="bb6e2-110">Tworzenie maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="bb6e2-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-111">Tworzy kilka maszyny wirtualne o wysokiej dostępności i konfiguracji równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="bb6e2-112">Tworzenie maszyny Wirtualnej, a następnie uruchom skrypt konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bb6e2-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-113">Tworzy maszynę wirtualną i używa hello Azure niestandardowego skryptu rozszerzenia tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="bb6e2-114">Utwórz maszynę Wirtualną i uruchomić konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="bb6e2-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-115">Tworzy maszynę wirtualną i używa hello konfiguracji żądanego stanu Azure (DSC) rozszerzenia tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="bb6e2-116">**Maszyny wirtualne sieci**</span><span class="sxs-lookup"><span data-stu-id="bb6e2-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="bb6e2-117">Bezpieczny ruch sieciowy między maszynami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="bb6e2-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-118">Tworzy dwie maszyny wirtualne, wszystkich powiązanych zasobów i grup zabezpieczeń sieci wewnętrznych i zewnętrznych (NSG).</span><span class="sxs-lookup"><span data-stu-id="bb6e2-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="bb6e2-119">**Bezpieczne maszyny wirtualne**</span><span class="sxs-lookup"><span data-stu-id="bb6e2-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="bb6e2-120">Szyfrowanie dysków maszyny Wirtualnej i danych</span><span class="sxs-lookup"><span data-stu-id="bb6e2-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-121">Tworzy usługi Azure Key Vault, klucz szyfrowania i nazwy głównej usługi, a następnie szyfruje maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="bb6e2-122">**Monitorowanie maszyn wirtualnych**</span><span class="sxs-lookup"><span data-stu-id="bb6e2-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="bb6e2-123">Monitor maszyny Wirtualnej w usłudze Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="bb6e2-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bb6e2-124">Tworzy maszynę wirtualną, instaluje agenta Operations Management Suite hello i rejestruje hello maszyny Wirtualnej w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="bb6e2-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
