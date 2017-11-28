---
title: "aaaValidate hello sieci Wirtualnej Azure toouse z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomake się, że sieci wirtualnej platformy Azure jest gotowy toouse z usługą Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="6f487-103">Sprawdź poprawność hello toouse sieci Wirtualnej platformy Azure z usługą Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6f487-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f487-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6f487-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6f487-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6f487-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6f487-106">Przed użyciem sieć Wirtualną platformy Azure z usługą Azure RemoteApp, może zaistnieć hello toovalidate sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f487-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="6f487-107">Pomaga to zapobiec występowaniu problemów z łącznością.</span><span class="sxs-lookup"><span data-stu-id="6f487-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="6f487-108">toovalidate sieci wirtualnej platformy Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6f487-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="6f487-109">Utwórz maszynę wirtualną platformy Azure w podsieci hello hello sieci Wirtualnej Azure ma toouse z usługą Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6f487-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="6f487-110">Połącz z toothat maszyny Wirtualnej, używając hello **Connect** opcji w portalu zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="6f487-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="6f487-111">Dołącz toohello maszyny wirtualnej hello tej samej domeny, które mają toouse z usługą Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6f487-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="6f487-112">Jeśli tworzysz kolekcję hybrydową, które łączy sieć lokalną tooyour przyłączyć hello domeny lokalnej tooyour maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f487-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="6f487-113">Jeśli to się powiedzie, hello sieci Wirtualnej platformy Azure jest gotowy toouse z usługą RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6f487-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="6f487-114">Aby uzyskać więcej informacji na temat przepływu pracy kolekcji hybrydowych end-to-end hello Zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="6f487-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="6f487-115">Jak tooplan sieci wirtualnej dla usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6f487-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="6f487-116">Tworzenie kolekcji hybrydowej</span><span class="sxs-lookup"><span data-stu-id="6f487-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="6f487-117">Wdrażanie usługi Azure RemoteApp kolekcji tooyour sieci wirtualnej platformy Azure (z obsługą usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="6f487-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

