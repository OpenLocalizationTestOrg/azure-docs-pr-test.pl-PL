---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych za pomocą hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="1cea1-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej z wykorzystaniem hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1cea1-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1cea1-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1cea1-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="1cea1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cea1-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="1cea1-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1cea1-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="1cea1-107">Portalu Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="1cea1-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="1cea1-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="1cea1-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="1cea1-109">Interfejs wiersza polecenia platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="1cea1-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1cea1-110">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="1cea1-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="1cea1-111">Możesz również [Zarządzanie statycznego prywatnego adresu IP w hello klasycznego modelu wdrażania](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1cea1-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="1cea1-112">Poniższe kroki przykładowe Hello oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="1cea1-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="1cea1-113">Jeśli kroki hello toorun wyświetlaną w tym dokumencie, należy najpierw utworzyć hello środowisko testowe opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1cea1-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="1cea1-114">Jak adresy toocreate Maszynę wirtualną do testowania statycznego prywatnego adresu IP</span><span class="sxs-lookup"><span data-stu-id="1cea1-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="1cea1-115">Nie można ustawić statycznego prywatnego adresu IP podczas tworzenia maszyny Wirtualnej w tryb wdrażania usługi Resource Manager hello hello przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1cea1-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="1cea1-116">Należy najpierw utworzyć hello maszyny Wirtualnej, tehn ustaw jej prywatnego adresu IP toobe statycznych.</span><span class="sxs-lookup"><span data-stu-id="1cea1-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="1cea1-117">toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet*, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="1cea1-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="1cea1-118">W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1cea1-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="1cea1-119">Kliknij przycisk **nowy** > **obliczeniowe** > **systemu Windows Server 2012 R2 Datacenter**, zwróć uwagę, że hello **wybierz model wdrożenia** listy już pokazuje **Resource Manager**, a następnie kliknij przycisk **Utwórz**, jak pokazano na poniższej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="1cea1-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="1cea1-121">W hello **podstawy** bloku, wprowadź nazwę hello hello toobe maszyny Wirtualnej utworzone (*DNS01* w naszym scenariuszu), hello konta administratora lokalnego i hasło, jak pokazano na poniższej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="1cea1-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Blok Podstawowe](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="1cea1-123">Upewnij się, że hello **lokalizacji** jest *środkowe stany USA*, następnie kliknij przycisk **wybierz istniejącą** w obszarze **grupy zasobów**, następnie kliknij przycisk **Grupy zasobów** ponownie, następnie kliknij przycisk *TestRG*, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Blok Podstawowe](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="1cea1-125">W hello **wybierz rozmiar** bloku, wybierz opcję **A1 standardowe**, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Wybierz rozmiar bloku](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="1cea1-127">W **ustawienia** bloku Utwórz hello się następujące właściwości są ustawiane są konfigurowane przy użyciu wartości hello poniżej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="1cea1-128">-**Konto magazynu**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="1cea1-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="1cea1-129">**Sieci**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="1cea1-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="1cea1-130">**Podsieci**: *frontonu*</span><span class="sxs-lookup"><span data-stu-id="1cea1-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Wybierz rozmiar bloku](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="1cea1-132">W hello **Podsumowanie** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="1cea1-133">Powiadomienie hello kafelka poniżej wyświetlane na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="1cea1-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="1cea1-135">Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1cea1-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="1cea1-136">tooview hello statycznych prywatne informacje o adresie IP dla hello się, że maszyna wirtualna utworzona z powyższych kroków hello wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="1cea1-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="1cea1-137">W portalu Azure, Azure hello, kliknij polecenie **PRZEGLĄDAJ wszystko** > **maszyn wirtualnych** > **DNS01** > **wszystkie ustawienia** > **interfejsy sieciowe** a następnie kliknij polecenie hello tylko interfejsu sieciowego na liście.</span><span class="sxs-lookup"><span data-stu-id="1cea1-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![Wdrażanie maszyny Wirtualnej kafelka](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="1cea1-139">W hello **interfejsu sieciowego** bloku, kliknij przycisk **wszystkie ustawienia** > **adresów IP** i hello powiadomienia **przypisania** i **Adres IP** wartości.</span><span class="sxs-lookup"><span data-stu-id="1cea1-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![Wdrażanie maszyny Wirtualnej kafelka](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="1cea1-141">Jak tooadd statycznego prywatnego adresu IP adresów tooan istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1cea1-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="1cea1-142">tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu powyższych kroków hello wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1cea1-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="1cea1-143">Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **statycznych** w obszarze **przypisania**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="1cea1-144">Typ *192.168.1.101* dla **adres IP**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="1cea1-146">Jeśli po kliknięciu przycisku **zapisać** można zauważyć, że przypisanie hello nadal jest ustawione zbyt**dynamiczne**, oznacza to, że wpisany adres IP hello jest już używana.</span><span class="sxs-lookup"><span data-stu-id="1cea1-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="1cea1-147">Spróbuj innego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="1cea1-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="1cea1-148">Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1cea1-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="1cea1-149">tooremove hello statycznego prywatnego adresu IP z powitalne maszyny Wirtualnej utworzone powyżej, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="1cea1-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="1cea1-150">Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **dynamiczne** w obszarze **przypisania**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1cea1-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cea1-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cea1-151">Next steps</span></span>
* <span data-ttu-id="1cea1-152">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="1cea1-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1cea1-153">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="1cea1-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1cea1-154">Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="1cea1-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

