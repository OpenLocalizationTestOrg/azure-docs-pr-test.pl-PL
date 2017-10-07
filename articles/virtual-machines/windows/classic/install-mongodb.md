---
title: aaaInstall MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall MongoDB na maszynie Wirtualnej platformy Azure utworzona z hello klasycznego modelu wdrażania systemem Windows Server."
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
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="f0f77-103">Instalowanie bazy danych MongoDB Windows maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f0f77-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0f77-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0f77-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f0f77-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="f0f77-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f0f77-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0f77-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f0f77-107">tooinstall oraz konfigurowania bazy danych MongoDB przy użyciu modelu wdrażania usługi Resource Manager hello, zobacz [w tym artykule](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="f0f77-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="f0f77-108">[Bazy danych MongoDB] [ MongoDB] jest popularnych open source, wysokiej wydajności bazę danych NoSQL.</span><span class="sxs-lookup"><span data-stu-id="f0f77-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="f0f77-109">W tym artykule prowadzi użytkownika przez proces tworzenia maszyny wirtualnej systemu Windows Server (VM) przy użyciu hello [portalu Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="f0f77-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="f0f77-110">Następnie utwórz i Dołącz toohello dysku danych maszyny Wirtualnej przed zainstalowaniem i skonfigurowaniem bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f0f77-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="f0f77-111">Jeśli masz istniejącą maszynę Wirtualną na platformie Azure, które chcesz toouse, można przejść bezpośrednio za[Instalowanie i Konfigurowanie bazy danych MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="f0f77-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="f0f77-112">Tworzenie maszyny wirtualnej z systemem Windows Server</span><span class="sxs-lookup"><span data-stu-id="f0f77-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="f0f77-113">Wykonaj te instrukcje toocreate maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f77-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="f0f77-114">Dodawanie punktu końcowego dla bazy danych MongoDB podczas tworzenia maszyny wirtualnej hello i skonfigurować w następujący sposób: go jako nazwa **Mongo**, użyj **TCP** jako protokół hello i ustaw zarówno hello portów publicznego i prywatnego zbyt**27017**.</span><span class="sxs-lookup"><span data-stu-id="f0f77-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="f0f77-115">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="f0f77-115">Attach a data disk</span></span>
<span data-ttu-id="f0f77-116">Magazyn tooprovide hello maszyny wirtualnej, dołączenie dysku danych i zainicjować go, aby można go używać systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f0f77-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="f0f77-117">Jeśli masz już dysk danych, można dołączyć istniejącego dysku, lub możesz dołączyć pusty dysk.</span><span class="sxs-lookup"><span data-stu-id="f0f77-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="f0f77-118">Aby uzyskać instrukcje na inicjowanie dysku hello, zobacz "jak: Zainicjuj nowy dysk danych w systemie Windows Server" w [jak tooattach danych na dysku maszyny wirtualnej systemu Windows tooa](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="f0f77-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="f0f77-119">Zainstalować i uruchomić na maszynie wirtualnej hello bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="f0f77-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="f0f77-120">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f0f77-120">Summary</span></span>
<span data-ttu-id="f0f77-121">W tym samouczku przedstawiono sposób toocreate maszyny wirtualnej z systemem Windows Server zdalnie połączyć tooit i dołączenie dysku danych.</span><span class="sxs-lookup"><span data-stu-id="f0f77-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="f0f77-122">Przedstawiono również sposób tooinstall i konfigurowanie maszyny wirtualnej z systemem Windows hello bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f0f77-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="f0f77-123">Można uzyskać dostęp bazy danych MongoDB hello systemu Windows maszyny wirtualnej przez następujące hello zaawansowanych tematów w hello [dokumentacją usługi MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="f0f77-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

