---
title: "Utwórz maszynę Wirtualną z statycznego publicznego adresu IP - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Maszynę wirtualną za pomocą statycznego publicznego adresu IP przy użyciu portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="85a89-103">Utwórz maszynę Wirtualną za pomocą statycznego publicznego adresu IP przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="85a89-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="85a89-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="85a89-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="85a89-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85a89-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="85a89-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="85a89-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="85a89-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="85a89-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="85a89-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="85a89-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="85a89-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="85a89-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="85a89-110">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów, które firma Microsoft zaleca w przypadku większości nowych wdrożeń zamiast klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="85a89-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="85a89-111">Utwórz maszynę Wirtualną z statycznego publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="85a89-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="85a89-112">Aby utworzyć Maszynę wirtualną za pomocą statycznego publicznego adresu IP w portalu Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="85a89-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="85a89-113">W przeglądarce przejdź do witryny [Azure Portal](https://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="85a89-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="85a89-114">W lewym górnym rogu portalu kliknij **nowy**>>**obliczeniowe**>**systemu Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="85a89-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="85a89-115">W **wybierz model wdrożenia** wybierz **Resource Manager** i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="85a89-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="85a89-116">W **podstawy** bloku, wprowadź informacje maszyny Wirtualnej, jak pokazano poniżej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="85a89-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Portal Azure — podstawy](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="85a89-118">W **wybierz rozmiar** bloku, kliknij przycisk **A1 standardowe** w sposób przedstawiony poniżej, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="85a89-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portal Azure — wybierz rozmiar](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="85a89-120">W **ustawienia** bloku, kliknij przycisk **publicznego adresu IP**, a następnie w **tworzenie publicznego adresu IP** bloku, w obszarze **przypisania**, kliknij przycisk **statycznych** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="85a89-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="85a89-121">A następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="85a89-121">And then click **OK**.</span></span>
   
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="85a89-123">W **ustawienia** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="85a89-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="85a89-124">Przegląd **Podsumowanie** bloku, jak pokazano poniżej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="85a89-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="85a89-126">Zobaczysz nowy Kafelek na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="85a89-126">Notice the new tile in your dashboard.</span></span>
   
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="85a89-128">Po utworzeniu maszyny Wirtualnej **ustawienia** w sposób przedstawiony poniżej zostanie wyświetlony blok</span><span class="sxs-lookup"><span data-stu-id="85a89-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

