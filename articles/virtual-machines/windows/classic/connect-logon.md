---
title: "Zaloguj się do klasycznej maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj portalu Azure do logowania się do systemu Windows maszyny wirtualnej utworzonej z klasycznym modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="03481-103">Logowanie do maszyny wirtualnej systemu Windows przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="03481-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="03481-104">W portalu Azure, użyj **Connect** przycisk, aby rozpocząć sesję pulpitu zdalnego i zaloguj się do maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="03481-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="03481-105">Czy chcesz połączyć z maszyną wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="03481-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="03481-106">Zobacz [jak zalogować się do maszyny wirtualnej z systemem Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="03481-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="03481-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="03481-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="03481-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="03481-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="03481-109">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="03481-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="03481-110">Aby uzyskać informacje o tym, jak zalogować się do maszyny Wirtualnej przy użyciu modelu Resource Manager, zobacz [tutaj](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03481-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="03481-111">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="03481-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="03481-112">Zaloguj się do Portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="03481-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="03481-113">Kliknij maszynę wirtualną, którą chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="03481-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="03481-114">Nazwa jest wyświetlana w **wszystkie zasoby** okienka.</span><span class="sxs-lookup"><span data-stu-id="03481-114">The name is listed in the **All resources** pane.</span></span>

    ![Lokalizacje wirtualne — komputera](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="03481-116">Kliknij przycisk **Connect** na pasku poleceń nad pulpitu nawigacyjnego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="03481-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![Połączenia dla maszyny wirtualnej](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="03481-118">Logowanie do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="03481-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="03481-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03481-119">Next steps</span></span>
* <span data-ttu-id="03481-120">Jeśli **Connect** przycisk jest nieaktywny lub występują inne problemy z połączeniem pulpitu zdalnego, spróbuj zresetować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="03481-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="03481-121">Kliknij przycisk **Zresetuj dostęp zdalny** z poziomu pulpitu nawigacyjnego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="03481-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Resetowanie zdalnego dostępu](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="03481-123">Problemy z hasłem spróbuj zresetować urządzenie.</span><span class="sxs-lookup"><span data-stu-id="03481-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="03481-124">Kliknij przycisk **resetowania hasła** wzdłuż lewej krawędzi wirtualnej maszyny pulpitu nawigacyjnego, w obszarze **pomocy technicznej i rozwiązywania problemów**.</span><span class="sxs-lookup"><span data-stu-id="03481-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Zresetuj hasło](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="03481-126">Te porady nie działa lub nie są potrzebne, zobacz [połączeń Rozwiązywanie problemów z pulpitu zdalnego do systemu Windows Azure maszyny wirtualnej](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03481-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="03481-127">W tym artykule przedstawiono sposób diagnozowania i rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="03481-127">This article walks you through diagnosing and resolving common problems.</span></span>
