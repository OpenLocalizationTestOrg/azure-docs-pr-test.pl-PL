---
title: "Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować istniejącą sieć wirtualną i podsieć, a następnie używać ich na maszynie wirtualnej z platformy Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="15af3-103">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="15af3-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="15af3-104">Jak opisano w artykule [dodać maszyny Wirtualnej z artefaktami do laboratorium](devtest-lab-add-vm-with-artifacts.md), podczas tworzenia maszyn wirtualnych w laboratorium, można określić skonfigurowanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="15af3-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="15af3-105">Jeden scenariusz w ten sposób jest konieczne dostęp do zasobów sieci corpnet z maszyn wirtualnych przy użyciu sieci wirtualnej, który został skonfigurowany za pomocą usługi ExpressRoute i sieci VPN typu lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="15af3-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="15af3-106">Poniższe sekcje przedstawiają sposób dodawania istniejącej sieci wirtualnej do ustawień sieci wirtualnej laboratorium, aby była ona dostępna do wyboru podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="15af3-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="15af3-107">Skonfiguruj sieć wirtualną dla laboratorium przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="15af3-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="15af3-108">W poniższych krokach objaśniono przez procedurę dodawania istniejącej sieci wirtualnej (i podsieci) do laboratorium, dzięki czemu można użyć podczas tworzenia maszyny Wirtualnej w tym samym laboratorium.</span><span class="sxs-lookup"><span data-stu-id="15af3-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="15af3-109">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="15af3-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="15af3-110">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy.</span><span class="sxs-lookup"><span data-stu-id="15af3-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="15af3-111">Z listy labs wybierz żądany laboratorium.</span><span class="sxs-lookup"><span data-stu-id="15af3-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="15af3-112">W bloku laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="15af3-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="15af3-113">W laboratorium **konfiguracji** bloku, wybierz opcję **sieci wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="15af3-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="15af3-114">Na **sieci wirtualnych** bloku, wyświetlić listę sieci wirtualne skonfigurowane dla bieżącego laboratorium, a także domyślne sieci wirtualnej utworzonym dla laboratorium.</span><span class="sxs-lookup"><span data-stu-id="15af3-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="15af3-115">Wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="15af3-115">Select **+ Add**.</span></span>
   
    ![Dodawanie istniejącej sieci wirtualnej do laboratorium](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="15af3-117">Na **sieci wirtualnej** bloku, wybierz opcję **[Wybierz sieć wirtualną]**.</span><span class="sxs-lookup"><span data-stu-id="15af3-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Wybierz istniejącą sieć wirtualną](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="15af3-119">Na **sieci wirtualnej wybierz** bloku, wybierz odpowiednią sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="15af3-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="15af3-120">Blok zawiera wszystkie sieci wirtualne, które są w tym samym regionie, w ramach subskrypcji jako laboratorium.</span><span class="sxs-lookup"><span data-stu-id="15af3-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="15af3-121">Po wybraniu sieci wirtualnej, nastąpi powrót do **sieci wirtualnej** kliknij podsieci na liście w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="15af3-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Lista podsieci](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="15af3-123">Blok podsieci laboratorium jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="15af3-123">The Lab Subnet blade is displayed.</span></span>

    ![Blok podsieci laboratorium](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="15af3-125">Określ **Nazwa podsieci laboratorium**.</span><span class="sxs-lookup"><span data-stu-id="15af3-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="15af3-126">Aby zezwolić na podsieci do użycia w laboratorium tworzenia maszyny Wirtualnej, wybierz **używany podczas tworzenia maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="15af3-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="15af3-127">Aby włączyć [udostępnionych publicznego adresu IP](devtest-lab-shared-ip.md), wybierz pozycję **Włącz udostępnione publicznego adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="15af3-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="15af3-128">Aby zezwolić na publiczne adresy IP w podsieci, wybierz **pozwala publicznego adresu IP tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="15af3-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="15af3-129">W **maksymalna maszyn wirtualnych dla użytkownika** pola, określ maksymalną maszyn wirtualnych dla poszczególnych użytkowników, dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="15af3-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="15af3-130">Jeśli chcesz nieograniczoną liczbę maszyn wirtualnych, pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="15af3-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="15af3-131">Wybierz **OK** zamknąć blok podsieci laboratorium.</span><span class="sxs-lookup"><span data-stu-id="15af3-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="15af3-132">Wybierz **zapisać** zamknąć bloku sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="15af3-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="15af3-133">Teraz, gdy skonfigurowano sieci wirtualnej, można wybrać podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="15af3-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="15af3-134">Aby sprawdzić, jak utworzyć Maszynę wirtualną i określ sieć wirtualną, zapoznaj się z artykułem [dodać maszyny Wirtualnej z artefaktami do laboratorium](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="15af3-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="15af3-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15af3-135">Next steps</span></span>
<span data-ttu-id="15af3-136">Po dodaniu żądanej sieci wirtualnej do laboratorium, następnym krokiem jest [Dodaj Maszynę wirtualną do laboratorium](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="15af3-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

