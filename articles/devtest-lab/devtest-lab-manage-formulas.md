---
title: "aaaManage formuły w usłudze Azure DevTest Labs toocreate maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate i Usuń formuły Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="56783-103">Zarządzanie formuły Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="56783-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="56783-104">W tym artykule przedstawiono sposób toocreate formuła z podstawowej (obrazu niestandardowego obrazu z witryny Marketplace i formułą) lub istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="56783-105">W tym artykule również przeprowadzi Cię przez zarządzanie istniejące formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="56783-106">Utwórz formułę</span><span class="sxs-lookup"><span data-stu-id="56783-106">Create a formula</span></span>
<span data-ttu-id="56783-107">Każda osoba mająca DevTest Labs *użytkowników* uprawnień jest możliwe toocreate maszyn wirtualnych przy użyciu formuły jako podstawy.</span><span class="sxs-lookup"><span data-stu-id="56783-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="56783-108">Istnieją dwa sposoby toocreate formuły:</span><span class="sxs-lookup"><span data-stu-id="56783-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="56783-109">Z podstawowej — należy użyć toodefine wszystkie właściwości hello hello formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="56783-110">Z istniejącego laboratorium VM - używany w toocreate formuły na podstawie hello ustawień z istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="56783-111">Aby uzyskać więcej informacji na temat dodawania użytkowników i uprawnień, zobacz [Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="56783-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="56783-112">Utwórz formułę z podstawowej</span><span class="sxs-lookup"><span data-stu-id="56783-112">Create a formula from a base</span></span>
<span data-ttu-id="56783-113">Witaj, wykonaj czynności pomocne hello proces tworzenia formuł z niestandardowego obrazu, obrazu z witryny Marketplace lub formułą.</span><span class="sxs-lookup"><span data-stu-id="56783-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="56783-114">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="56783-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="56783-115">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="56783-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="56783-116">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="56783-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="56783-117">W bloku hello laboratorium, wybierz **formuły (podstaw wielokrotnego użytku)**.</span><span class="sxs-lookup"><span data-stu-id="56783-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formuły menu](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="56783-119">Na powitania **formuły** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="56783-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Dodawanie formuły](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="56783-121">Na powitania **wybierz podstawowej** bloku base wybierz hello (obrazu niestandardowego obrazu z witryny Marketplace i formuły) z którego mają zostać toocreate hello formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Lista podstawowa](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="56783-123">Na powitania **utworzyć formuły** bloku, określ hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="56783-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="56783-124">**Nazwa formuły** — wprowadź nazwę dla formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="56783-125">Ta wartość jest wyświetlana w hello listy obrazów podstawowej podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="56783-126">Nazwa Hello jest weryfikowana go, a jeśli jest on nieprawidłowy komunikat wskazuje hello wymagania dotyczące prawidłową nazwę.</span><span class="sxs-lookup"><span data-stu-id="56783-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="56783-127">**Opis elementu** — wpisz zrozumiały opis dla formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="56783-128">Ta wartość jest dostępna z menu kontekstowego hello formuły, podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="56783-129">**Nazwa użytkownika** — wprowadź nazwę użytkownika, któremu udzielono uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="56783-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="56783-130">**Hasło** — wprowadź - lub wybierz z listy rozwijanej hello - wartość, która jest skojarzona z hello hasło, mają toouse dla hello określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="56783-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="56783-131">Aby uzyskać więcej informacji na temat kluczy tajnych hello, zobacz [Azure DevTest Labs: tajne magazynie osobistym](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="56783-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="56783-132">**Typ dysku maszyny wirtualnej** — określ albo dysk twardy (dysk twardy) lub tooindicate dysków SSD (SSD) typ dysku magazynu, który jest dozwolony dla maszyn wirtualnych hello udostępniane przy użyciu tego obrazu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="56783-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="56783-133">** Maszyny wirtualnej rozmiar ** — wybierz jedną z hello wstępnie zdefiniowane elementy, które Określ hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="56783-134">**Artefakty** -hello wybierz tooopen **dodać artefakty** bloku, w którym wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz.</span><span class="sxs-lookup"><span data-stu-id="56783-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="56783-135">Aby uzyskać więcej informacji na temat artefaktów, zobacz [artefakty zarządzania maszyny Wirtualnej w usłudze Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="56783-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="56783-136">**Zaawansowane ustawienia** -hello wybierz tooopen **zaawansowane** bloku, w którym skonfigurować hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="56783-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="56783-137">**Sieć wirtualna** — Określ hello potrzeby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="56783-138">**Podsieci** — Określ podsieć hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="56783-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="56783-139">**Adres IP** -określić adresy hello Public, Private lub udostępnione IP.</span><span class="sxs-lookup"><span data-stu-id="56783-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="56783-140">Aby uzyskać więcej informacji na temat udostępnionych adresów IP, zobacz [omówienie udostępnionych adresów IP w usłudze Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="56783-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="56783-141">**Przydziel tej maszynie claimable** — co maszyna "claimable" oznacza, że go nie zostaną przypisane prawa własności w czasie hello tworzenia.</span><span class="sxs-lookup"><span data-stu-id="56783-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="56783-142">Zamiast tego użytkownicy laboratorium będą mogli tootake własność ("roszczenie") hello maszyny w bloku hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="56783-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="56783-143">**Obraz** -wyświetlana nazwa obrazu podstawowego hello wybranego na powitania poprzedniego bloku.</span><span class="sxs-lookup"><span data-stu-id="56783-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Utwórz formułę](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="56783-145">Wybierz **Utwórz** toocreate hello formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="56783-146">Tworzona formuła hello wyświetla na liście hello na powitania **formuły** bloku.</span><span class="sxs-lookup"><span data-stu-id="56783-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="56783-147">Utwórz formułę z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="56783-147">Create a formula from a VM</span></span>
<span data-ttu-id="56783-148">Witaj następujące kroki przedstawiono hello proces tworzenia formułę opartą na istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56783-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="56783-149">toocreate formuły z maszyny Wirtualnej, hello maszyny Wirtualnej musi być utworzony po 30 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="56783-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="56783-150">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="56783-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="56783-151">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="56783-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="56783-152">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="56783-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="56783-153">W laboratorium hello **omówienie** bloku, wybierz hello maszyny Wirtualnej, z którego chcesz toocreate hello formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Maszyny wirtualne laboratoria](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="56783-155">W bloku hello wirtualna wybierz **utworzyć formuły (base wielokrotnego użytku)**.</span><span class="sxs-lookup"><span data-stu-id="56783-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Utwórz formułę](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="56783-157">Na powitania **utworzyć formuły** bloku, wprowadź **nazwa** i **opis** dla nowej formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Tworzenie formuły bloku](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="56783-159">Wybierz **OK** toocreate hello formuły.</span><span class="sxs-lookup"><span data-stu-id="56783-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="56783-160">Zmodyfikuj formułę</span><span class="sxs-lookup"><span data-stu-id="56783-160">Modify a formula</span></span>
<span data-ttu-id="56783-161">toomodify formuły, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="56783-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="56783-162">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="56783-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="56783-163">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="56783-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="56783-164">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="56783-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="56783-165">W bloku hello laboratorium, wybierz **formuły (podstaw wielokrotnego użytku)**.</span><span class="sxs-lookup"><span data-stu-id="56783-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formuły menu](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="56783-167">Na powitania **formuły laboratorium** bloku, wybierz hello formuły mają toomodify.</span><span class="sxs-lookup"><span data-stu-id="56783-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="56783-168">Na powitania **zaktualizować formułę** bloku, dokonaj edycji hello potrzebne, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="56783-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="56783-169">Usuwanie formuły</span><span class="sxs-lookup"><span data-stu-id="56783-169">Delete a formula</span></span>
<span data-ttu-id="56783-170">toodelete formuły, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="56783-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="56783-171">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="56783-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="56783-172">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="56783-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="56783-173">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="56783-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="56783-174">W laboratorium hello **ustawienia** bloku, wybierz opcję **formuły**.</span><span class="sxs-lookup"><span data-stu-id="56783-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Formuły menu](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="56783-176">Na powitania **formuły laboratorium** bloku, wybierz hello wielokropka toohello rogu formuła hello mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="56783-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Formuły menu](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="56783-178">W menu kontekstowym hello formuły, wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="56783-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Menu kontekstowe formuły](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="56783-180">Wybierz **tak** okno dialogowe potwierdzenia usunięcia toohello.</span><span class="sxs-lookup"><span data-stu-id="56783-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="56783-181">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="56783-181">Related blog posts</span></span>
* [<span data-ttu-id="56783-182">Niestandardowe obrazy lub formuł?</span><span class="sxs-lookup"><span data-stu-id="56783-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="56783-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56783-183">Next steps</span></span>
<span data-ttu-id="56783-184">Po utworzeniu formułę do użycia podczas tworzenia maszyny Wirtualnej, następnym krokiem hello jest zbyt[Dodawanie maszyny Wirtualnej laboratorium tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="56783-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

