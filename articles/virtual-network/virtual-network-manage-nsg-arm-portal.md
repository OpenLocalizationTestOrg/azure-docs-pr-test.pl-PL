---
title: "grupy NSG aaaManage przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage istniejących grup NSG przy użyciu hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="9c113-103">Zarządzanie za pomocą portalu hello grupy NSG</span><span class="sxs-lookup"><span data-stu-id="9c113-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c113-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9c113-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="9c113-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c113-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="9c113-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c113-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9c113-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c113-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c113-108">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9c113-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="9c113-109">Pobieranie informacji</span><span class="sxs-lookup"><span data-stu-id="9c113-109">Retrieve Information</span></span>
<span data-ttu-id="9c113-110">Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.</span><span class="sxs-lookup"><span data-stu-id="9c113-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="9c113-111">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="9c113-111">View existing NSGs</span></span>

<span data-ttu-id="9c113-112">tooview wszystkich istniejących grup NSG w ramach subskrypcji, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-113">W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c113-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="9c113-114">Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="9c113-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="9c113-116">Sprawdź listę hello grup NSG w hello **sieciowej grupy zabezpieczeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c113-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="9c113-118">Widok grup NSG, w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="9c113-118">View NSGs in a resource group</span></span>

<span data-ttu-id="9c113-119">tooview hello lista grup NSG w hello **NSG zarządcy zasobów** grupy zasobów, pełny hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-120">Kliknij przycisk **grup zasobów >** > **NSG zarządcy zasobów** > **...** .</span><span class="sxs-lookup"><span data-stu-id="9c113-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="9c113-122">Hello listy zasobów, szukać elementów Wyświetlanie hello NSG ikony, jak pokazano w hello **zasobów** bloku poniżej.</span><span class="sxs-lookup"><span data-stu-id="9c113-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="9c113-124">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="9c113-124">List all rules for an NSG</span></span>

<span data-ttu-id="9c113-125">tooview hello reguły NSG o nazwie **frontonu NSG**pełnego hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-126">Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="9c113-127">W hello **ustawienia** , kliknij pozycję **reguły zabezpieczeń dla ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="9c113-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="9c113-129">Witaj **reguły zabezpieczeń dla ruchu przychodzącego** bloku jest wyświetlana, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="9c113-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="9c113-131">W hello **ustawienia** , kliknij pozycję **reguł zabezpieczeń dla ruchu wychodzącego** toosee hello reguł dla ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9c113-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9c113-132">reguły domyślne tooview, kliknij przycisk hello **domyślne zasady** ikona u góry bloku hello, który wyświetla reguły hello hello.</span><span class="sxs-lookup"><span data-stu-id="9c113-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="9c113-133">Wyświetlanie grup NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="9c113-133">View NSGs associations</span></span>

<span data-ttu-id="9c113-134">tooview hello jakie zasoby **frontonu NSG** grupa NSG jest pełną, powiąż z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-135">Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="9c113-136">W hello **ustawienia** , kliknij pozycję **podsieci** tooview podsieci, które są skojarzone toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="9c113-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="9c113-138">W hello **ustawienia** , kliknij pozycję **interfejsy sieciowe** tooview co karty sieciowe są skojarzone toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="9c113-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="9c113-139">Zarządzaj regułami</span><span class="sxs-lookup"><span data-stu-id="9c113-139">Manage rules</span></span>
<span data-ttu-id="9c113-140">Można dodawać reguły tooan istniejące grupy NSG, edytować istniejące zasady i Usuń reguły.</span><span class="sxs-lookup"><span data-stu-id="9c113-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="9c113-141">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="9c113-141">Add a rule</span></span>
<span data-ttu-id="9c113-142">tooadd, dzięki czemu reguły **przychodzących** tooport ruchu **443** z dowolnej maszyny toohello **NSG frontonu** NSG, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-143">Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c113-144">W hello **ustawienia** , kliknij pozycję **reguły zabezpieczeń dla ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="9c113-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="9c113-145">W hello **reguły zabezpieczeń dla ruchu przychodzącego** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9c113-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="9c113-146">Następnie w hello **Dodaj regułę zabezpieczeń dla ruchu przychodzącego** bloku, wypełnij hello wartości, jak pokazano poniżej, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c113-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="9c113-148">Po kilku sekundach zauważyć hello nową regułę w hello **reguły zabezpieczeń dla ruchu przychodzącego** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c113-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="9c113-150">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="9c113-150">Change a rule</span></span>
<span data-ttu-id="9c113-151">Reguła hello toochange utworzone powyżej tooallow ruchu przychodzącego ruchu z hello **Internet** hello pełną, tylko następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-152">Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c113-153">W hello **ustawienia** , kliknij pozycję reguły hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="9c113-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="9c113-154">W hello **Zezwalaj https** bloku, zmień hello **źródła** właściwości, jak pokazano poniżej, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="9c113-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="9c113-156">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="9c113-156">Delete a rule</span></span>

<span data-ttu-id="9c113-157">toodelete hello reguły utworzone powyżej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-158">Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c113-159">W hello **ustawienia** , kliknij pozycję reguły hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="9c113-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="9c113-160">W hello **Zezwalaj https** bloku, kliknij przycisk **usunąć**, a następnie kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="9c113-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="9c113-162">Zarządzanie skojarzenia</span><span class="sxs-lookup"><span data-stu-id="9c113-162">Manage associations</span></span>
<span data-ttu-id="9c113-163">Możesz skojarzyć toosubnets NSG i kart interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9c113-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="9c113-164">Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.</span><span class="sxs-lookup"><span data-stu-id="9c113-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="9c113-165">Kojarzenie grupy NSG tooa karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="9c113-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="9c113-166">Witaj tooassociate **frontonu NSG** NSG toohello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-167">Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c113-168">W hello **ustawienia** , kliknij pozycję **interfejsy sieciowe** > **skojarzyć** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="9c113-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="9c113-170">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="9c113-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="9c113-171">Witaj toodissociate **frontonu NSG** grupy NSG z hello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-172">Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="9c113-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="9c113-173">W hello **TestNICWeb1** bloku, kliknij przycisk **zmiany zabezpieczeń...**   >  **Brak**.</span><span class="sxs-lookup"><span data-stu-id="9c113-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="9c113-175">Umożliwia także tego bloku tooassociate hello kart tooany istniejące grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="9c113-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="9c113-176">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="9c113-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="9c113-177">Witaj toodissociate **frontonu NSG** grupy NSG z hello **frontonu** podsieci, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-178">Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="9c113-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="9c113-179">W hello **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń**  >  **Brak**.</span><span class="sxs-lookup"><span data-stu-id="9c113-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="9c113-181">W hello **frontonu** bloku, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="9c113-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="9c113-183">Kojarzenie grupy NSG podsieci tooa</span><span class="sxs-lookup"><span data-stu-id="9c113-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="9c113-184">Witaj tooassociate **frontonu NSG** NSG toohello **FronEnd** ponownie podsieci, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c113-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="9c113-185">Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="9c113-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="9c113-186">W hello **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń**  >  **Frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="9c113-187">W hello **frontonu** bloku, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="9c113-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="9c113-188">Można również skojarzyć podsieci tooa grupy NSG z thh NSG **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c113-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="9c113-189">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="9c113-189">Delete an NSG</span></span>
<span data-ttu-id="9c113-190">Grupy NSG można usuwać tylko, jeśli nie został skojarzony tooany zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c113-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="9c113-191">toodelete grupy NSG, pełną hello następujące kroki:.</span><span class="sxs-lookup"><span data-stu-id="9c113-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="9c113-192">Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **Frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="9c113-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c113-193">W hello **ustawienia** bloku, kliknij przycisk **interfejsy sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="9c113-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="9c113-194">W przypadku wszystkie karty sieciowe na liście kliknij hello karty Sieciowej i wykonaj krok 2 w [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="9c113-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="9c113-195">Powtórz krok 3 dla każdej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="9c113-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="9c113-196">W hello **ustawienia** bloku, kliknij przycisk **podsieci**.</span><span class="sxs-lookup"><span data-stu-id="9c113-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="9c113-197">Jeśli ma żadnych podsieci na liście, kliknij hello podsieci i wykonaj kroki 2 i 3 w [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="9c113-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="9c113-198">Przewija po lewej stronie toohello **frontonu NSG** bloku, następnie kliknij przycisk **usunąć** > **tak**.</span><span class="sxs-lookup"><span data-stu-id="9c113-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="9c113-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c113-200">Next steps</span></span>
* <span data-ttu-id="9c113-201">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="9c113-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
