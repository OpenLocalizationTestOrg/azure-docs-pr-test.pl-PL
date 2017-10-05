---
title: "Nawiązywanie połączenia z maszyną wirtualną z systemem Windows Server | Microsoft Docs"
description: "Dowiedz się, jak nawiązać połączenie z maszyną wirtualną z systemem Windows oraz zalogować się do niej za pomocą witryny Azure Portal i modelu wdrażania przy użyciu usługi Azure Resource Manager."
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
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="a09ec-103">Sposób nawiązywania połączenia z maszyną wirtualną platformy Azure z systemem Windows oraz logowania się do niej</span><span class="sxs-lookup"><span data-stu-id="a09ec-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="a09ec-104">Korzystając z przycisku **Połącz** w witrynie Azure Portal, uruchomisz sesję pulpitu zdalnego z poziomu pulpitu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a09ec-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="a09ec-105">Najpierw nawiążesz połączenie z maszyną wirtualną, a następnie zalogujesz się.</span><span class="sxs-lookup"><span data-stu-id="a09ec-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="a09ec-106">W przypadku próby nawiązania połączenia z maszyną wirtualną z systemem Windows z poziomu komputera Mac konieczne jest zainstalowanie klienta RDP dla komputerów Mac, takiego jak [Pulpit zdalny Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="a09ec-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="a09ec-107">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="a09ec-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="a09ec-108">Jeśli jeszcze tego nie zrobiono, zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a09ec-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a09ec-109">W menu Centrum kliknij pozycję **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="a09ec-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="a09ec-110">Wybierz maszynę wirtualną z listy.</span><span class="sxs-lookup"><span data-stu-id="a09ec-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="a09ec-111">W bloku maszyny wirtualnej kliknij pozycję **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="a09ec-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Zrzut ekranu witryny Azure Portal pokazujący sposób nawiązywania połączenia z maszyną wirtualną.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="a09ec-113">Jeśli przycisk **Połącz** w portalu jest nieaktywny i nie masz połączenia typu [ExpressRoute](../../expressroute/expressroute-introduction.md) lub Sieć VPN typu [lokacja do lokacji](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) z platformą Azure, musisz utworzyć i przypisać maszynie wirtualnej publiczny adres IP przed użyciem pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="a09ec-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="a09ec-114">Więcej informacji o [publicznych adresach IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a09ec-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="a09ec-115">Logowanie do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a09ec-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="a09ec-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a09ec-116">Next steps</span></span>
<span data-ttu-id="a09ec-117">Jeśli podczas próby połączenia wystąpiły problemy, zobacz [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Rozwiązywanie problemów z połączeniami pulpitu zdalnego).</span><span class="sxs-lookup"><span data-stu-id="a09ec-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a09ec-118">W tym artykule przedstawiono sposób diagnozowania i rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="a09ec-118">This article walks you through diagnosing and resolving common problems.</span></span>

