---
title: "aaaAdd claimable laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd laboratorium tooa claimable maszyny wirtualnej w usłudze Azure DevTest Labs"
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
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="0c29d-103">Dodaj claimable laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0c29d-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="0c29d-104">Dodaj claimable laboratorium tooa maszyny Wirtualnej w podobny sposób toohow można [dodać maszyny Wirtualnej standardowego](devtest-lab-add-vm.md) — z *podstawowej* czyli albo [niestandardowego obrazu](devtest-lab-create-template.md), [formuła](devtest-lab-manage-formulas.md), lub [obrazu z witryny Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="0c29d-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="0c29d-105">W tym samouczku przedstawiono przy użyciu hello Azure tooadd portalu claimable laboratorium tooa maszyny Wirtualnej w usłudze DevTest Labs i przedstawia proces hello użytkownik wykonuje hello tooclaim maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0c29d-106">W przypadku wdrożenia maszyn wirtualnych laboratorium za pośrednictwem [szablonów usługi Azure Resource Manager](devtest-lab-create-environment-from-arm.md), claimable maszyn wirtualnych można utworzyć Ustawianie hello **allowClaim** tootrue właściwości w sekcji właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="0c29d-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="0c29d-107">Kroki tooadd claimable laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0c29d-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="0c29d-108">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="0c29d-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="0c29d-109">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="0c29d-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="0c29d-110">Z listy hello labs, wybierz hello laboratorium, w której chcesz toocreate hello claimable maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="0c29d-111">W laboratorium hello **omówienie** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0c29d-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="0c29d-113">Na powitania **wybierz podstawowej** bloku, wybierz podstawa hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="0c29d-114">Na powitania **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej hello w hello **nazwę maszyny wirtualnej** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0c29d-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="0c29d-116">Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="0c29d-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="0c29d-117">Jeśli chcesz, aby toouse hasła przechowywane w Twojej [tajny magazynu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), wybierz pozycję **używać hasła zapisane**i określ wartości klucza, który odpowiada tooyour hasło.</span><span class="sxs-lookup"><span data-stu-id="0c29d-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="0c29d-118">W przeciwnym razie wprowadź hasło w polu tekstowym hello etykietą **wpisz wartość**.</span><span class="sxs-lookup"><span data-stu-id="0c29d-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="0c29d-119">Witaj **typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla hello maszyn wirtualnych w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="0c29d-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="0c29d-120">Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z hello wstępnie zdefiniowane elementy, które określić hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="0c29d-121">Wybierz **artefakty** i z listy hello artefaktów, wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz.</span><span class="sxs-lookup"><span data-stu-id="0c29d-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="0c29d-122">Nowe Labs tooDevTest lub konfigurowanie artefaktów, zobacz toohello [Dodawanie istniejących tooa artefaktu maszyny Wirtualnej](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="0c29d-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="0c29d-123">Wybierz **Zaawansowane ustawienia** opcje i wygaśnięcia opcje sieciowe tooconfigure hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="0c29d-124">W obszarze **oświadczeń opcje**, wybierz **tak** toomake hello maszyny claimable.</span><span class="sxs-lookup"><span data-stu-id="0c29d-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![Wybierz hello toomake claimable maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="0c29d-126">Tooview lub skopiuj hello szablonu usługi Azure Resource Manager, zobacz toohello [szablonu Zapisz Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) , a następnie wróć tutaj po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="0c29d-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="0c29d-127">Wybierz **Utwórz** tooadd hello określony laboratorium toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="0c29d-128">Blok laboratorium Hello Wyświetla stan hello tworzenie hello VM - najpierw jako **tworzenie**, następnie jako **systemem** po hello maszyna wirtualna została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="0c29d-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="0c29d-129">Przy użyciu claimable maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0c29d-129">Using a claimable VM</span></span>

<span data-ttu-id="0c29d-130">Użytkownika można oświadczeń żadnej maszyny Wirtualnej z listy "Claimable maszyny wirtualne" hello, wykonując jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="0c29d-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="0c29d-131">Z listy hello "Claimable maszyny wirtualne" u dołu bloku omówienie laboratorium hello hello, kliknij prawym przyciskiem myszy na jednym z hello maszyn wirtualnych na liście hello i wybierz polecenie **maszyny oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="0c29d-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![Żądanie claimable określonej maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="0c29d-133">U góry hello hello **omówienie** bloku, wybierz **uzyskania**.</span><span class="sxs-lookup"><span data-stu-id="0c29d-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="0c29d-134">Losowe maszyny wirtualnej jest przypisane z listy hello claimable maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0c29d-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![Żądanie żadnej claimable maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="0c29d-136">Po użytkownika oświadczeń maszyny Wirtualnej, przenieść w górę do listy "Moje maszyny wirtualne" i nie jest już claimable przez innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0c29d-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c29d-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c29d-137">Next steps</span></span>
* <span data-ttu-id="0c29d-138">Raz hello maszyna wirtualna została utworzona, można połączyć toohello maszyny Wirtualnej, wybierając **Connect** w bloku hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0c29d-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="0c29d-139">Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="0c29d-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
