---
title: "Dodaj claimable maszyny Wirtualnej do laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać claimable maszyny wirtualnej do laboratorium w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="cfded-103">Dodaj claimable maszyny Wirtualnej do laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="cfded-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="cfded-104">Dodaj Maszynę wirtualną claimable laboratorium w podobny sposób jak możesz [dodać standardowe maszyny Wirtualnej](devtest-lab-add-vm.md) — z *podstawowej* czyli albo [niestandardowego obrazu](devtest-lab-create-template.md), [formuła](devtest-lab-manage-formulas.md) , lub [obrazu z witryny Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="cfded-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="cfded-105">Ten samouczek przeprowadzi Cię przez dodawanie claimable maszyny Wirtualnej do laboratorium w usłudze DevTest Labs przy użyciu portalu Azure i przedstawiono proces się, że użytkownik wykonuje przejąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="cfded-106">W przypadku wdrożenia maszyn wirtualnych laboratorium za pośrednictwem [szablonów usługi Azure Resource Manager](devtest-lab-create-environment-from-arm.md), można utworzyć claimable maszyn wirtualnych, ustawiając **allowClaim** właściwości na wartość true w sekcji właściwości.</span><span class="sxs-lookup"><span data-stu-id="cfded-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="cfded-107">Kroki, aby dodać claimable maszyny Wirtualnej do laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="cfded-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="cfded-108">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cfded-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="cfded-109">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy.</span><span class="sxs-lookup"><span data-stu-id="cfded-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="cfded-110">Z listy labs wybierz laboratorium, w którym chcesz utworzyć claimable maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="cfded-111">W laboratorium **omówienie** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cfded-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="cfded-113">Na **wybierz podstawowej** bloku, wybierz podstawowy dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="cfded-114">Na **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej w **nazwę maszyny wirtualnej** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cfded-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="cfded-116">Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="cfded-117">Jeśli chcesz skorzystać z hasła przechowywane w Twojej [tajny magazynu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), wybierz pozycję **używać hasła zapisane**i określ wartości klucza, który odpowiada klucz tajny (hasło).</span><span class="sxs-lookup"><span data-stu-id="cfded-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="cfded-118">W przeciwnym razie wprowadź hasło w polu tekstowym etykietą **wpisz wartość**.</span><span class="sxs-lookup"><span data-stu-id="cfded-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="cfded-119">**Typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="cfded-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="cfded-120">Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z wstępnie zdefiniowane elementy, które Określ rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego maszyny wirtualnej do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="cfded-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="cfded-121">Wybierz **artefakty** i na liście artefaktów, wybierz i skonfiguruj artefaktów, które chcesz dodać do obrazu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="cfded-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="cfded-122">Jeśli nowych użytkowników programu DevTest Labs lub konfigurowanie artefaktów, zapoznaj się [Dodaj istniejący artefakt do maszyny Wirtualnej](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="cfded-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="cfded-123">Wybierz **Zaawansowane ustawienia** Aby skonfigurować opcje wygaśnięcia i Opcje sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="cfded-124">W obszarze **oświadczeń opcje**, wybierz **tak** dokonanie claimable komputera.</span><span class="sxs-lookup"><span data-stu-id="cfded-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Wybierz claimable maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="cfded-126">Jeśli chcesz wyświetlić lub skopiuj szablon usługi Azure Resource Manager, zapoznaj się [szablonu Zapisz Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) , a następnie wróć tutaj po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="cfded-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="cfded-127">Wybierz **Utwórz** dodać określoną maszynę Wirtualną do laboratorium.</span><span class="sxs-lookup"><span data-stu-id="cfded-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="cfded-128">Blok laboratorium Wyświetla stan tworzenia maszyny Wirtualnej — najpierw jako **tworzenie**, następnie jako **systemem** po uruchomieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="cfded-129">Przy użyciu claimable maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cfded-129">Using a claimable VM</span></span>

<span data-ttu-id="cfded-130">Użytkownik może oświadczeń żadnej maszyny Wirtualnej z listy "Claimable maszyny wirtualne", wykonując jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cfded-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="cfded-131">Z listy "Claimable maszyny wirtualnej" w dolnej części bloku omówienie laboratorium należy utworzyć, kliknij prawym przyciskiem myszy na jednym z maszyn wirtualnych na liście, a następnie wybierz pozycję **maszyny oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="cfded-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Żądanie claimable określonej maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="cfded-133">W górnej części **omówienie** bloku, wybierz **uzyskania**.</span><span class="sxs-lookup"><span data-stu-id="cfded-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="cfded-134">Losowe maszyny wirtualnej jest przypisane z listy claimable maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cfded-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Żądanie żadnej claimable maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="cfded-136">Po użytkownika oświadczeń maszyny Wirtualnej, przenieść w górę do listy "Moje maszyny wirtualne" i nie jest już claimable przez innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cfded-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfded-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cfded-137">Next steps</span></span>
* <span data-ttu-id="cfded-138">Po utworzeniu maszyny Wirtualnej można Połącz się z maszyną Wirtualną, wybierając **Connect** w bloku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cfded-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="cfded-139">Eksploruj [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="cfded-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
