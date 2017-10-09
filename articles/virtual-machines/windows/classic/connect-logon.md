---
title: aaaLog na tooa klasyczne maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Użyj hello toolog portalu Azure na maszynie wirtualnej Windows tooa utworzone za pomocą hello klasycznego modelu wdrażania."
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
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="61cd5-103">Zaloguj się na tooa maszyny wirtualnej systemu Windows przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="61cd5-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="61cd5-104">W portalu Azure hello, użyj hello **Connect** przycisk toostart sesję pulpitu zdalnego i zaloguj się na tooa maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="61cd5-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="61cd5-105">Czy chcesz tooa tooconnect maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="61cd5-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="61cd5-106">Zobacz [jak toolog na tooa maszyny wirtualnej z systemem Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="61cd5-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="61cd5-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="61cd5-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="61cd5-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="61cd5-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="61cd5-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61cd5-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="61cd5-110">Aby dowiedzieć się, jak toolog na tooa maszynę Wirtualną przy użyciu hello Resource Manager modelu, zobacz [tutaj](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61cd5-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="61cd5-111">Połącz toohello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61cd5-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="61cd5-112">Zaloguj się toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="61cd5-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="61cd5-113">Polecenie hello maszyny wirtualnej, które mają tooaccess.</span><span class="sxs-lookup"><span data-stu-id="61cd5-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="61cd5-114">Nazwa Hello jest wyświetlana w hello **wszystkie zasoby** okienka.</span><span class="sxs-lookup"><span data-stu-id="61cd5-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Lokalizacje wirtualne — komputera](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="61cd5-116">Kliknij przycisk **Connect** na pasku poleceń hello nad hello maszyny wirtualnej z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="61cd5-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Połączenia dla maszyny wirtualnej hello](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="61cd5-118">Zaloguj się na maszynie wirtualnej toohello</span><span class="sxs-lookup"><span data-stu-id="61cd5-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="61cd5-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61cd5-119">Next steps</span></span>
* <span data-ttu-id="61cd5-120">Jeśli hello **Connect** przycisk jest nieaktywny lub występują inne problemy z połączeniem pulpitu zdalnego hello, spróbuj zresetować hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61cd5-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="61cd5-121">Kliknij przycisk **Zresetuj dostęp zdalny** z poziomu pulpitu nawigacyjnego hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd5-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Resetowanie zdalnego dostępu](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="61cd5-123">Problemy z hasłem spróbuj zresetować urządzenie.</span><span class="sxs-lookup"><span data-stu-id="61cd5-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="61cd5-124">Kliknij przycisk **resetowania hasła** wzdłuż hello lewej krawędzi pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **pomocy technicznej i rozwiązywania problemów**.</span><span class="sxs-lookup"><span data-stu-id="61cd5-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Zresetuj hasło](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="61cd5-126">Te porady nie działa lub nie są potrzebne, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny wirtualnej z systemem Windows Azure](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61cd5-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="61cd5-127">W tym artykule przedstawiono sposób diagnozowania i rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="61cd5-127">This article walks you through diagnosing and resolving common problems.</span></span>
