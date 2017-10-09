---
title: "grupy zabezpieczeń sieci aaaManage - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage sieciowych grup zabezpieczeń za pomocą hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="f6ce3-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f6ce3-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f6ce3-104">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f6ce3-105">Możesz również [tworzenia grup NSG w hello klasycznego modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f6ce3-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="f6ce3-106">w powyższym scenariuszu hello na podstawie próbek Hello PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="f6ce3-107">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="f6ce3-108">Witaj kroków poniżej użyj **NSG zarządcy zasobów** jako nazwę hello hello zasobów grupy hello szablonu został wdrożony.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="f6ce3-109">Utwórz hello NSG frontonu NSG</span><span class="sxs-lookup"><span data-stu-id="f6ce3-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="f6ce3-110">Witaj toocreate **frontonu NSG** NSG, jak pokazano w scenariuszu hello powyżej, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="f6ce3-111">W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="f6ce3-112">Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="f6ce3-114">W hello **sieciowej grupy zabezpieczeń** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="f6ce3-116">W hello **Utwórz grupę zabezpieczeń sieci** bloku Utwórz grupy NSG o nazwie *frontonu NSG* w hello *NSG zarządcy zasobów* grupy zasobów, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="f6ce3-118">Tworzenie reguł w istniejącej sieciowej grupie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="f6ce3-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="f6ce3-119">reguły toocreate w istniejącej grupy NSG z hello portalu Azure, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="f6ce3-120">Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="f6ce3-121">Na liście hello grup NSG, kliknij **frontonu NSG** > **reguły zabezpieczeń dla ruchu przychodzącego**</span><span class="sxs-lookup"><span data-stu-id="f6ce3-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portal Azure — frontonu NSG](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="f6ce3-123">Lista hello **reguły zabezpieczeń dla ruchu przychodzącego**, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portal Azure — Dodaj regułę](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="f6ce3-125">W hello **Dodaj regułę zabezpieczeń dla ruchu przychodzącego** bloku Utwórz reguły o nazwie *zasada sieci web* z priorytet *200* zezwalania na dostęp za pośrednictwem *TCP* tooport *80* tooany maszyny Wirtualnej z dowolnego źródła, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="f6ce3-126">Zwróć uwagę, że większość tych ustawień są wartościami domyślnymi już.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portal Azure — ustawienia reguły](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="f6ce3-128">Po kilku sekundach zobaczysz hello nową regułę w hello NSG.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Portal Azure — nową regułę](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="f6ce3-130">Powtórz kroki too6 toocreate regułę ruchu przychodzącego o nazwie *reguły protokołu rdp* z priorytet *250* zezwalania na dostęp za pośrednictwem *TCP* tooport *3389* tooany maszyny Wirtualnej z dowolnego źródła.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="f6ce3-131">Skojarz hello NSG toohello frontonu podsieci</span><span class="sxs-lookup"><span data-stu-id="f6ce3-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="f6ce3-132">Kliknij przycisk **Przeglądaj >** > **grup zasobów** > **NSG zarządcy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="f6ce3-133">W hello **NSG zarządcy zasobów** bloku, kliknij przycisk **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portal Azure — TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="f6ce3-135">W hello **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń**  >  **Frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portal Azure — ustawienia podsieci](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="f6ce3-137">W hello **frontonu** bloku, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portal Azure — ustawienia podsieci](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="f6ce3-139">Utwórz hello NSG wewnętrznej bazy danych grupy NSG</span><span class="sxs-lookup"><span data-stu-id="f6ce3-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="f6ce3-140">toocreate hello **zaplecza NSG** NSG i powiązać ją toohello **zaplecza** podsieci, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="f6ce3-141">Hello Powtórz kroki opisane w temacie [hello Utwórz NSG frontonu NSG](#Create-the-NSG-FrontEnd-NSG) toocreate o nazwie grupy NSG *wewnętrznej bazy danych grupy NSG*</span><span class="sxs-lookup"><span data-stu-id="f6ce3-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="f6ce3-142">Hello Powtórz kroki opisane w temacie [tworzenia reguł w istniejącej grupy NSG](#Create-rules-in-an-existing-NSG) toocreate hello **przychodzących** reguły w poniższej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="f6ce3-143">Reguła ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="f6ce3-143">Inbound rule</span></span> | <span data-ttu-id="f6ce3-144">Reguła ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="f6ce3-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portal Azure — reguły dla ruchu przychodzącego](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal Azure — Reguła ruchu wychodzącego](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="f6ce3-147">Hello Powtórz kroki opisane w temacie [skojarzyć podsieci frontonu toohello NSG hello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **zaplecza NSG** NSG toohello **zaplecza** podsieci.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ce3-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6ce3-148">Next Steps</span></span>
* <span data-ttu-id="f6ce3-149">Dowiedz się, jak za[Zarządzanie istniejących grup NSG](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f6ce3-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="f6ce3-150">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

