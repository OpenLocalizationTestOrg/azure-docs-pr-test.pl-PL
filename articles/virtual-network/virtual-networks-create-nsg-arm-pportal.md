---
title: "Utwórz sieciowej grupy zabezpieczeń - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i wdrożyć grup zabezpieczeń sieci przy użyciu portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 865032f350735d35668bb199ccf1ef3f0fae81de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="83e4c-103">Tworzenie grup zabezpieczeń za pomocą portalu Azure w sieci</span><span class="sxs-lookup"><span data-stu-id="83e4c-103">Create network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="83e4c-104">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="83e4c-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="83e4c-105">Możesz również [tworzenia grup NSG w klasycznym modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="83e4c-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="83e4c-106">W powyższym scenariuszu na podstawie próbek PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="83e4c-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="83e4c-107">Jeśli chcesz uruchomić polecenia wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), kliknij przycisk **wdrażanie na platformie Azure**, Zastąp domyślne wartości parametrów, jeśli to konieczne i postępuj zgodnie z instrukcjami w portalu.</span><span class="sxs-lookup"><span data-stu-id="83e4c-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="83e4c-108">Kroki użyj **NSG zarządcy zasobów** jako nazwę grupy zasobów, szablon został wdrożony.</span><span class="sxs-lookup"><span data-stu-id="83e4c-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="83e4c-109">Tworzenie grupy NSG frontonu NSG</span><span class="sxs-lookup"><span data-stu-id="83e4c-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="83e4c-110">Aby utworzyć **frontonu NSG** NSG, jak pokazano w scenariuszu powyżej, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="83e4c-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="83e4c-111">W przeglądarce przejdź do strony http://portal.azure.com i w razie potrzeby zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83e4c-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="83e4c-112">Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="83e4c-114">W **sieciowej grupy zabezpieczeń** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="83e4c-116">W **Utwórz grupę zabezpieczeń sieci** bloku Utwórz grupy NSG o nazwie *frontonu NSG* w *NSG zarządcy zasobów* grupy zasobów, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="83e4c-118">Tworzenie reguł w istniejącej sieciowej grupie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="83e4c-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="83e4c-119">Aby utworzyć reguły w istniejącej grupy NSG z portalu Azure, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="83e4c-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="83e4c-120">Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="83e4c-121">Na liście grup NSG, kliknij **frontonu NSG** > **reguły zabezpieczeń dla ruchu przychodzącego**</span><span class="sxs-lookup"><span data-stu-id="83e4c-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portal Azure — frontonu NSG](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="83e4c-123">Na liście **reguły zabezpieczeń dla ruchu przychodzącego**, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portal Azure — Dodaj regułę](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="83e4c-125">W **Dodaj regułę zabezpieczeń dla ruchu przychodzącego** bloku Utwórz reguły o nazwie *zasada sieci web* z priorytet *200* zezwalania na dostęp za pośrednictwem *TCP* do portu *80* do żadnej maszyny Wirtualnej z dowolnego źródła, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="83e4c-126">Zwróć uwagę, że większość tych ustawień są wartościami domyślnymi już.</span><span class="sxs-lookup"><span data-stu-id="83e4c-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portal Azure — ustawienia reguły](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="83e4c-128">Po kilku sekundach zostanie wyświetlone nowe zasady w grupie NSG.</span><span class="sxs-lookup"><span data-stu-id="83e4c-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Portal Azure — nową regułę](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="83e4c-130">Powtórz kroki od 6 do utworzenia reguły ruchu przychodzącego o nazwie *reguły protokołu rdp* z priorytet *250* zezwalania na dostęp za pośrednictwem *TCP* do portu *3389* do żadnej maszyny Wirtualnej z dowolnego źródła.</span><span class="sxs-lookup"><span data-stu-id="83e4c-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="83e4c-131">Kojarzenie sieciowej grupy zabezpieczeń z podsiecią FrontEnd</span><span class="sxs-lookup"><span data-stu-id="83e4c-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="83e4c-132">Kliknij przycisk **Przeglądaj >** > **grup zasobów** > **NSG zarządcy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="83e4c-133">W **NSG zarządcy zasobów** bloku, kliknij przycisk **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portal Azure — TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="83e4c-135">W **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń** > **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portal Azure — ustawienia podsieci](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="83e4c-137">W **frontonu** bloku, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="83e4c-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portal Azure — ustawienia podsieci](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="83e4c-139">Tworzenie grupy NSG wewnętrznej bazy danych grupy NSG</span><span class="sxs-lookup"><span data-stu-id="83e4c-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="83e4c-140">Aby utworzyć **zaplecza NSG** NSG i powiązać ją do **wewnętrznej bazy danych** podsieci, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="83e4c-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="83e4c-141">Powtórz kroki [utworzyć NSG frontonu NSG](#Create-the-NSG-FrontEnd-NSG) do utworzenia grupy NSG o nazwie *wewnętrznej bazy danych grupy NSG*</span><span class="sxs-lookup"><span data-stu-id="83e4c-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="83e4c-142">Powtórz kroki [tworzenia reguł w istniejącej grupy NSG](#Create-rules-in-an-existing-NSG) utworzyć **przychodzących** reguły w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="83e4c-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="83e4c-143">Reguła ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="83e4c-143">Inbound rule</span></span> | <span data-ttu-id="83e4c-144">Reguła ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="83e4c-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portal Azure — reguły dla ruchu przychodzącego](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal Azure — Reguła ruchu wychodzącego](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="83e4c-147">Powtórz kroki [kojarzenie grupy NSG do podsieci frontonu](#Associate-the-NSG-to-the-FrontEnd-subnet) do skojarzenia **zaplecza NSG** grupy NSG **zaplecza** podsieci.</span><span class="sxs-lookup"><span data-stu-id="83e4c-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83e4c-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83e4c-148">Next Steps</span></span>
* <span data-ttu-id="83e4c-149">Dowiedz się, jak [Zarządzanie istniejących grup NSG](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="83e4c-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="83e4c-150">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="83e4c-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

