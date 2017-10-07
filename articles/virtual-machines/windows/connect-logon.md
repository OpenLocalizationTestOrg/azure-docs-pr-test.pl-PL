---
title: tooa aaaConnect maszyny Wirtualnej systemu Windows Server | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect i logowanie przy użyciu maszyny Wirtualnej systemu Windows tooa hello Azure portal hello Resource Manager wdrażania modelu."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="10745-103">Jak dziennika na tooan wirtualnej platformy Azure i tooconnect komputera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="10745-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="10745-104">Użyjesz hello **Connect** przycisk hello Azure toostart portalu sesji pulpitu zdalnego (RDP) na pulpicie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="10745-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="10745-105">Najpierw połącz toohello maszyny wirtualnej, a następnie zaloguj się na.</span><span class="sxs-lookup"><span data-stu-id="10745-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="10745-106">Jeśli próbujesz tooa tooconnect maszyny Wirtualnej systemu Windows z Mac, należy tooinstall klientem RDP dla komputerów Mac, takich jak [pulpitu zdalnego firmy Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="10745-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="10745-107">Połącz toohello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10745-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="10745-108">Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="10745-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="10745-109">W menu Centrum powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="10745-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="10745-110">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="10745-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="10745-111">W bloku hello hello maszyny wirtualnej, kliknij **Connect**.</span><span class="sxs-lookup"><span data-stu-id="10745-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Zrzut ekranu przedstawiający portal Azure hello jak tooyour tooconnect maszyny Wirtualnej.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="10745-113">Jeśli hello **Connect** przycisk w portalu hello jest nieaktywny i nie jesteś tooAzure połączonych za pośrednictwem [Express Route](../../expressroute/expressroute-introduction.md) lub [sieci VPN typu lokacja-lokacja](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) połączenia, należy toocreate i przypisać maszynie Wirtualnej publiczny adres IP, zanim będzie możliwe użycie protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="10745-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="10745-114">Więcej informacji o [publicznych adresach IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="10745-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="10745-115">Zaloguj się na maszynie wirtualnej toohello</span><span class="sxs-lookup"><span data-stu-id="10745-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="10745-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10745-116">Next steps</span></span>
<span data-ttu-id="10745-117">Jeśli wystąpiły problemy podczas próby tooconnect, zobacz [połączeń pulpitu zdalnego Rozwiązywanie problemów z](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10745-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="10745-118">W tym artykule przedstawiono sposób diagnozowania i rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="10745-118">This article walks you through diagnosing and resolving common problems.</span></span>

