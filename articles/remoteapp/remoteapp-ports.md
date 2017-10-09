---
title: "aaaList toowhitelist porty i adresy URL dla usługi Azure RemoteApp wdrożony w sieci wirtualnych klienta | Dokumentacja firmy Microsoft"
description: "Dowiedz się, które porty i adresy URL tooconfigure potrzebne do komunikacji za pośrednictwem usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="10272-103">Lista dostępu toopermit porty i adresy URL dla usługi Azure RemoteApp wdrożonych klientów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10272-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="10272-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="10272-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="10272-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="10272-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="10272-106">Jeśli wdrażasz kolekcji usługi Azure RemoteApp w chmurze czy hybrydowa w sieć wirtualną (VNET), przejrzyj następujące informacje o portach hello.</span><span class="sxs-lookup"><span data-stu-id="10272-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="10272-107">Aby uzyskać więcej informacji o sieciach wirtualnych, przeczytaj [omówienie sieci wirtualnych](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10272-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="10272-108">Jeśli po utworzeniu grupy zabezpieczeń sieci (NSG) Ograniczanie ruchu toohello sieci wirtualnej zasobów w kolekcji, upewnij się, że hello następujące porty są dozwolone za pomocą zasad zabezpieczeń hello na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10272-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="10272-109">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, przeczytaj [co to jest grupa zabezpieczeń sieci? (NSG) ](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="10272-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="10272-110">Usługa Azure RemoteApp podsieci musi punkty końcowe toothese dostępu i adresy URL:</span><span class="sxs-lookup"><span data-stu-id="10272-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="10272-111">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="10272-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="10272-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="10272-112">*.servicebus.net</span></span>
* <span data-ttu-id="10272-113">https://*.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="10272-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="10272-114">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="10272-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="10272-115">https://*RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="10272-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="10272-116">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="10272-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="10272-117">Wychodzące: TCP: TCP: 443, 9351, 9352, 10101 10175</span><span class="sxs-lookup"><span data-stu-id="10272-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="10272-118">Opcjonalne — UDP: 10201 10275</span><span class="sxs-lookup"><span data-stu-id="10272-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="10272-119">Klienci usługi Azure RemoteApp muszą uzyskać dostęp do punktów końcowych toothese i adres URL:</span><span class="sxs-lookup"><span data-stu-id="10272-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="10272-120">Przez klientów, które oznacza I hello komputerów osobistych, urządzeń itp. tej osoby Użyj tooconnect toohello aplikacje wdrożone w hello kolekcji usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="10272-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="10272-121">https://telemetry.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="10272-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="10272-122">https://*.RemoteApp.windowsazure.com (opcjonalne porty UDP hello są dla tego adresu)</span><span class="sxs-lookup"><span data-stu-id="10272-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="10272-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="10272-123">https://login.windows.net</span></span>  
* <span data-ttu-id="10272-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="10272-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="10272-125">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="10272-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="10272-126">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="10272-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="10272-127">Wychodzące: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="10272-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="10272-128">Opcjonalne - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="10272-128">Optional - UDP: 3391</span></span> 

