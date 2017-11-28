---
title: 'Usuwanie bramy sieci wirtualnej: portalu Azure: Resource Manager | Dokumentacja firmy Microsoft'
description: "Usuń bramę sieci wirtualnej przy użyciu portalu Azure w modelu wdrażania usługi Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="2d226-103">Usuwanie bramy sieci wirtualnej przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="2d226-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d226-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2d226-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="2d226-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d226-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="2d226-106">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="2d226-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="2d226-107">Istnieje kilka różnych metod, które można wykonać, gdy chcesz usunąć bramę sieci wirtualnej dla konfiguracji bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="2d226-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="2d226-108">Jeśli chcesz usunąć wszystkie elementy i rozpocząć od początku, tak jak w przypadku środowiska testowego, można usunąć grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d226-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="2d226-109">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie.</span><span class="sxs-lookup"><span data-stu-id="2d226-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="2d226-110">Jest to metoda, jest zalecane tylko jeśli nie chcesz zachować zasoby w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d226-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="2d226-111">Nie można selektywnie usunąć tylko kilka zasobów, przy użyciu tej metody.</span><span class="sxs-lookup"><span data-stu-id="2d226-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="2d226-112">Jeśli chcesz zachować niektóre zasoby w grupie zasobów, usuwanie bramy sieci wirtualnej staje się nieco bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="2d226-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="2d226-113">Aby można było usunąć bramę sieci wirtualnej, należy najpierw usunąć wszystkie zasoby, które są zależne od bramy.</span><span class="sxs-lookup"><span data-stu-id="2d226-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="2d226-114">Kroki, które należy wykonać są zależne od typu połączenia, które zostały utworzone i zasoby zależne, dla każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="2d226-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="2d226-115">Usuwanie bramy VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="2d226-115">Delete a VPN gateway</span></span>

<span data-ttu-id="2d226-116">Aby usunąć bramę sieci wirtualnej, należy najpierw usunąć wszystkie zasoby, które odnoszą się do bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d226-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="2d226-117">Zasoby muszą zostać usunięte w określonej kolejności z powodu zależności.</span><span class="sxs-lookup"><span data-stu-id="2d226-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="2d226-118">W tym momencie Brama sieci wirtualnej została usunięta.</span><span class="sxs-lookup"><span data-stu-id="2d226-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="2d226-119">Następne kroki pomóc usunąć wszystkie zasoby, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="2d226-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="2d226-120">Aby usunąć bramę sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="2d226-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="2d226-121">W **wszystkie zasoby**, zlokalizuj bram sieci lokalnej, które zostały skojarzone z każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="2d226-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="2d226-122">Na **omówienie** bloku dla bramy sieci lokalnej, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2d226-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="2d226-123">Aby usunąć zasób adres publiczny adres IP dla bramy</span><span class="sxs-lookup"><span data-stu-id="2d226-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="2d226-124">W **wszystkie zasoby**, zlokalizuj zasób adres publiczny adres IP, który został skojarzony z bramą.</span><span class="sxs-lookup"><span data-stu-id="2d226-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="2d226-125">Jeśli brama sieci wirtualnej był aktywny aktywny, zostanie wyświetlony dwa publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="2d226-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="2d226-126">Na **omówienie** dla publicznego adresu IP kliknij pozycję **usunąć**, następnie **tak** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="2d226-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="2d226-127">Aby usunąć podsieć bramy</span><span class="sxs-lookup"><span data-stu-id="2d226-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="2d226-128">W **wszystkie zasoby**, zlokalizuj sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d226-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="2d226-129">Na **podsieci** bloku, kliknij przycisk **GatewaySubnet**, następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2d226-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="2d226-130">Kliknij przycisk **tak** aby upewnić się, że chcesz usunąć podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="2d226-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="2d226-131"><a name="deleterg"></a>Usuwanie bramy sieci VPN przez usunięcie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2d226-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="2d226-132">Jeśli nie są dane dotyczące poszczególnych zasobów w grupie zasobów i po prostu chcesz zacząć od nowa, należy usunąć całej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d226-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="2d226-133">Jest to szybko Usuń całą.</span><span class="sxs-lookup"><span data-stu-id="2d226-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="2d226-134">Poniższe kroki dotyczą tylko modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d226-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="2d226-135">W **wszystkie zasoby**Znajdź grupę zasobów i kliknij, aby otworzyć blok.</span><span class="sxs-lookup"><span data-stu-id="2d226-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="2d226-136">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="2d226-136">Click **Delete**.</span></span> <span data-ttu-id="2d226-137">W bloku Delete wyświetlania wykorzystywanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d226-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="2d226-138">Upewnij się, że chcesz usunąć wszystkich tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d226-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="2d226-139">Jeśli nie, wykonaj kroki w [usunąć bramę sieci VPN](#deletegw) w górnej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d226-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="2d226-140">Aby kontynuować, wpisz nazwę grupy zasobów, które chcesz usunąć, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2d226-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>