---
title: Instalowanie bazy danych MongoDB Windows maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zainstalować bazy danych MongoDB na maszynie Wirtualnej platformy Azure utworzonych za pomocą klasycznego modelu wdrażania systemem Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 6b5af18d02fd508a21cdc21b38b1c16e79f07ecb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="f3519-103">Instalowanie bazy danych MongoDB Windows maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f3519-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f3519-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f3519-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f3519-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f3519-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f3519-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f3519-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f3519-107">Aby zainstalować i skonfigurować bazy danych MongoDB przy użyciu modelu wdrażania usługi Resource Manager, zobacz [w tym artykule](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="f3519-107">To install and configure MongoDB using the Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="f3519-108">[Bazy danych MongoDB] [ MongoDB] jest popularnych open source, wysokiej wydajności bazę danych NoSQL.</span><span class="sxs-lookup"><span data-stu-id="f3519-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="f3519-109">W tym artykule prowadzi użytkownika przez proces tworzenia maszyny wirtualnej (VM) systemu Windows Server przy użyciu [portalu Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="f3519-109">This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal].</span></span> <span data-ttu-id="f3519-110">Następnie utwórz i Dołącz dysku danych do maszyny Wirtualnej przed zainstalowaniem i skonfigurowaniem bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f3519-110">You then create and attach a data disk to the VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="f3519-111">Jeśli masz istniejącą maszynę Wirtualną na platformie Azure, którego chcesz użyć, można przejść bezpośrednio do [Instalowanie i Konfigurowanie bazy danych MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="f3519-111">If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="f3519-112">Tworzenie maszyny wirtualnej z systemem Windows Server</span><span class="sxs-lookup"><span data-stu-id="f3519-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="f3519-113">Wykonaj te instrukcje, aby utworzyć maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f3519-113">Follow these instructions to create a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="f3519-114">Dodawanie punktu końcowego dla bazy danych MongoDB podczas tworzenia maszyny wirtualnej i skonfigurować w następujący sposób: Nazwa go jako **Mongo**, użyj **TCP** jako protokół i Ustaw porty publiczny i prywatny **27017**.</span><span class="sxs-lookup"><span data-stu-id="f3519-114">You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="f3519-115">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="f3519-115">Attach a data disk</span></span>
<span data-ttu-id="f3519-116">Zapewnianie magazynowania dla maszyny wirtualnej, dołączenie dysku danych, a następnie zainicjować, tak aby można go używać systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f3519-116">To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="f3519-117">Jeśli masz już dysk danych, można dołączyć istniejącego dysku, lub możesz dołączyć pusty dysk.</span><span class="sxs-lookup"><span data-stu-id="f3519-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="f3519-118">Aby uzyskać instrukcje dotyczące inicjowania dysku, zobacz "jak: Zainicjuj nowy dysk danych w systemie Windows Server" w [jak można dołączyć dysku danych do maszyny wirtualnej systemu Windows](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="f3519-118">For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-the-virtual-machine"></a><span data-ttu-id="f3519-119">Zainstaluj i uruchom bazy danych MongoDB na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f3519-119">Install and run MongoDB on the virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="f3519-120">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f3519-120">Summary</span></span>
<span data-ttu-id="f3519-121">W tym samouczku przedstawiono sposób tworzenia maszyny wirtualnej z systemem Windows Server, zdalnie nawiązać z nim i dołączenie dysku danych.</span><span class="sxs-lookup"><span data-stu-id="f3519-121">In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.</span></span>  <span data-ttu-id="f3519-122">Przedstawiono również sposób instalowania i konfigurowania bazy danych MongoDB na maszynie wirtualnej z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="f3519-122">You also learned how to install and configure MongoDB on the Windows-based virtual machine.</span></span> <span data-ttu-id="f3519-123">Na maszynie wirtualnej z systemem Windows można uzyskać dostęp bazy danych MongoDB, wykonując następujące tematy Zaawansowane w [dokumentacją usługi MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="f3519-123">You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

