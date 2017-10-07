---
title: "aaaConfigure sieci wirtualnej w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure istniejącej sieci wirtualnej i podsieci i używać ich na maszynie wirtualnej z platformy Azure DevTest Labs"
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
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="6ff25-103">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6ff25-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="6ff25-104">Zgodnie z opisem w artykule hello [dodać maszyny Wirtualnej z laboratorium tooa artefakty](devtest-lab-add-vm-with-artifacts.md), podczas tworzenia maszyn wirtualnych w laboratorium, można określić skonfigurowanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6ff25-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="6ff25-105">Jeden scenariusz w ten sposób jest, jeśli potrzebujesz tooaccess zasobami sieci corpnet z maszyn wirtualnych przy użyciu hello sieci wirtualnej, który został skonfigurowany za pomocą usługi ExpressRoute i sieci VPN typu lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="6ff25-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="6ff25-106">Witaj poniższe sekcje przedstawiają sposób tooadd istniejącej sieci wirtualnej do ustawień sieci wirtualnej laboratorium, tak aby była dostępna toochoose podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6ff25-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="6ff25-107">Skonfiguruj sieć wirtualną dla laboratorium hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6ff25-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="6ff25-108">Witaj kolejnych krokach objaśniono sposób przez procedurę dodawania istniejącego wirtualnego sieci (i podsieci) tooa laboratorium, dzięki czemu można użyć podczas tworzenia maszyny Wirtualnej w hello tego samego laboratorium.</span><span class="sxs-lookup"><span data-stu-id="6ff25-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="6ff25-109">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6ff25-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6ff25-110">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="6ff25-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="6ff25-111">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="6ff25-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="6ff25-112">W bloku hello laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="6ff25-113">W laboratorium hello **konfiguracji** bloku, wybierz opcję **sieci wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="6ff25-114">Na powitania **sieci wirtualnych** bloku, wyświetlić listę sieci wirtualne skonfigurowane dla hello bieżącym laboratorium, a także hello domyślną sieć wirtualna, która jest tworzona dla laboratorium.</span><span class="sxs-lookup"><span data-stu-id="6ff25-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="6ff25-115">Wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-115">Select **+ Add**.</span></span>
   
    ![Dodaj istniejącego laboratorium tooyour sieci wirtualnej](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="6ff25-117">Na powitania **sieci wirtualnej** bloku, wybierz opcję **[Wybierz sieć wirtualną]**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Wybierz istniejącą sieć wirtualną](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="6ff25-119">Na powitania **sieci wirtualnej wybierz** bloku, wybierz hello żądanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6ff25-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="6ff25-120">Hello bloku pokazuje wszystkie sieci wirtualne hello, które są w obszarze hello sam region w subskrypcji hello jako hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="6ff25-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="6ff25-121">Po wybraniu sieci wirtualnej, są zwracane toohello **sieci wirtualnej** kliknij podsieci hello liście hello u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="6ff25-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Lista podsieci](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="6ff25-123">Blok podsieci laboratorium Hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="6ff25-123">hello Lab Subnet blade is displayed.</span></span>

    ![Blok podsieci laboratorium](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="6ff25-125">Określ **Nazwa podsieci laboratorium**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="6ff25-126">Wybierz tooallow toobe podsieci, używane w laboratorium tworzenia maszyny Wirtualnej, **używany podczas tworzenia maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="6ff25-127">tooenable [udostępnionych publicznego adresu IP](devtest-lab-shared-ip.md), wybierz pozycję **Włącz udostępnione publicznego adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="6ff25-128">Wybierz tooallow publicznych adresów IP w podsieci, **pozwala publicznego adresu IP tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="6ff25-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="6ff25-129">W hello **maksymalna maszyn wirtualnych dla użytkownika** Określ hello maksymalną maszyn wirtualnych dla poszczególnych użytkowników, dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="6ff25-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="6ff25-130">Jeśli chcesz nieograniczoną liczbę maszyn wirtualnych, pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="6ff25-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="6ff25-131">Wybierz **OK** tooclose hello podsieci laboratorium bloku.</span><span class="sxs-lookup"><span data-stu-id="6ff25-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="6ff25-132">Wybierz **zapisać** bloku sieci wirtualnej hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="6ff25-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="6ff25-133">Teraz, gdy hello sieci wirtualnej jest skonfigurowany, można wybrać podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6ff25-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="6ff25-134">toosee jak toocreate maszyny Wirtualnej i określ sieć wirtualną, zobacz artykuł toohello [dodać maszyny Wirtualnej z laboratorium tooa artefakty](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6ff25-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6ff25-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ff25-135">Next steps</span></span>
<span data-ttu-id="6ff25-136">Po dodaniu hello potrzeby sieci wirtualnej laboratorium tooyour hello następnym krokiem jest zbyt[Dodawanie maszyny Wirtualnej laboratorium tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6ff25-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

