---
title: "aaaManage zasad laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodefine laboratorium zasad, takich jak wirtualna rozmiar maksymalny maszyn wirtualnych dla poszczególnych użytkowników i zamykania automatyzacji."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="05a86-103">Zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="05a86-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="05a86-104">Azure DevTest Labs umożliwia kontrolowanie kosztów i zminimalizować odpady w Twojej labs przez Zarządzanie zasadami (ustawienia) dla każdego laboratorium.</span><span class="sxs-lookup"><span data-stu-id="05a86-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="05a86-105">W tym artykule opisano krok po kroku szczegółowo sposób tooset każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="05a86-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="05a86-106">Zestaw dozwolone rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="05a86-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="05a86-107">Witaj zasady dla hello ustawienie dozwolone rozmiary maszyn wirtualnych pomaga laboratorium toominimize odpady włączając toospecify rozmiarów maszyn wirtualnych, które są dozwolone w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="05a86-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="05a86-108">Jeśli zasada ta jest aktywna, tylko rozmiary maszyn wirtualnych z tej listy można toocreate używanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="05a86-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="05a86-109">W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **dozwolone rozmiary maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="05a86-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Rozmiary maszyn wirtualnych dozwolonych](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="05a86-111">Wybierz **na** tooenable tych zasad i **poza** toodisable go.</span><span class="sxs-lookup"><span data-stu-id="05a86-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="05a86-112">Po włączeniu tych zasad, wybierz rozmiarów maszyn wirtualnych, które mogą zostać utworzone w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="05a86-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="05a86-113">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="05a86-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="05a86-114">Zestaw maszyn wirtualnych dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="05a86-114">Set virtual machines per user</span></span>
<span data-ttu-id="05a86-115">Witaj zasady dla **maszyn wirtualnych dla użytkownika** pozwala toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="05a86-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="05a86-116">Jeśli użytkownik próbuje toocreate lub oświadczeń maszyny Wirtualnej, gdy limit użytkowników hello zostaną spełnione, komunikat o błędzie wskazuje powitalne tej maszyny Wirtualnej nie może być utworzone/żądane.</span><span class="sxs-lookup"><span data-stu-id="05a86-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="05a86-117">W laboratorium hello **konfiguracji i zasadach** menu, wybierz opcję **maszyn wirtualnych dla użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="05a86-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Maszyny wirtualne na użytkownika](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="05a86-119">Wybierz **tak** toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="05a86-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="05a86-120">Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="05a86-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="05a86-121">W przypadku wybrania **tak**, wprowadź wartość liczbową wskazujący hello maksymalną liczbę maszyn wirtualnych, które można utworzyć ani przejęte przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="05a86-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="05a86-122">Wybierz **tak** toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD (dysk SSD).</span><span class="sxs-lookup"><span data-stu-id="05a86-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="05a86-123">Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="05a86-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="05a86-124">W przypadku wybrania **tak**, wprowadź wartość wskazującą maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przy użyciu dysków SSD hello.</span><span class="sxs-lookup"><span data-stu-id="05a86-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="05a86-125">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="05a86-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="05a86-126">Zestaw maszyn wirtualnych dla laboratorium</span><span class="sxs-lookup"><span data-stu-id="05a86-126">Set virtual machines per lab</span></span>
<span data-ttu-id="05a86-127">Witaj zasady dla **maszyn wirtualnych dla laboratorium** pozwala toospecify hello maksymalną liczbę maszyn wirtualnych, które można utworzyć hello bieżącym laboratorium.</span><span class="sxs-lookup"><span data-stu-id="05a86-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="05a86-128">Jeśli użytkownik próbuje toocreate maszyny Wirtualnej, gdy limit laboratorium hello zostaną spełnione, komunikat o błędzie wskazuje hello, że nie można utworzyć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05a86-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="05a86-129">W laboratorium hello **konfiguracji i zasadach** menu, wybierz opcję **maszyn wirtualnych dla laboratorium**.</span><span class="sxs-lookup"><span data-stu-id="05a86-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Maszyn wirtualnych dla laboratorium](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="05a86-131">Wybierz **tak** toolimit hello liczbę maszyn wirtualnych dla laboratorium.</span><span class="sxs-lookup"><span data-stu-id="05a86-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="05a86-132">Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych dla laboratorium, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="05a86-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="05a86-133">W przypadku wybrania **tak**, wprowadź wartość liczbową wskazujący hello maksymalną liczbę maszyn wirtualnych, które można utworzyć ani przejęte przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="05a86-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="05a86-134">Wybierz **tak** toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD (dysk SSD).</span><span class="sxs-lookup"><span data-stu-id="05a86-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="05a86-135">Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="05a86-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="05a86-136">W przypadku wybrania **tak**, wprowadź wartość wskazującą maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przy użyciu dysków SSD hello.</span><span class="sxs-lookup"><span data-stu-id="05a86-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="05a86-137">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="05a86-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="05a86-138">Ustaw automatyczne zamykanie</span><span class="sxs-lookup"><span data-stu-id="05a86-138">Set auto-shutdown</span></span>
<span data-ttu-id="05a86-139">zasady automatycznego zamykania Hello pomaga laboratorium toominimize odpady zezwalając czasu hello toospecify, zamykania maszyn wirtualnych w tym laboratorium.</span><span class="sxs-lookup"><span data-stu-id="05a86-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="05a86-140">W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **automatyczne zamykanie**.</span><span class="sxs-lookup"><span data-stu-id="05a86-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Automatyczne zamykanie](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="05a86-142">Wybierz **na** tooenable tych zasad i **poza** toodisable go.</span><span class="sxs-lookup"><span data-stu-id="05a86-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="05a86-143">Po włączeniu tych zasad, należy określić hello tooshut godziny (i strefy czasowej) w dół wszystkich maszyn wirtualnych w bieżącym laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="05a86-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="05a86-144">Określ **tak** lub **nr** dla toosend opcji hello toohello przed 15 minut powiadomień określona czasu automatycznego zamykania.</span><span class="sxs-lookup"><span data-stu-id="05a86-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="05a86-145">Jeśli określisz **tak**, wprowadź powiadomienie hello tooreceive punktu końcowego adresu URL elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="05a86-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="05a86-146">Aby uzyskać więcej informacji na temat elementów webhook, zobacz [tworzenia elementu webhook lub funkcja interfejsu API Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="05a86-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="05a86-147">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="05a86-147">Select **Save**.</span></span>

    <span data-ttu-id="05a86-148">Domyślnie po włączeniu ta zasada dotyczy maszyn wirtualnych tooall w bieżącym laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="05a86-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="05a86-149">tooremove tego ustawienia z określonej maszyny Wirtualnej, otwórz blok hello maszyny Wirtualnej i zmień jego **automatyczne zamykanie** ustawienie</span><span class="sxs-lookup"><span data-stu-id="05a86-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="05a86-150">Ustaw automatyczne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="05a86-150">Set auto-start</span></span>
<span data-ttu-id="05a86-151">zasady automatycznego uruchamiania Hello umożliwia toospecify hello maszyn wirtualnych w bieżącym laboratorium hello powinna być uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="05a86-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="05a86-152">W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="05a86-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Automatyczne uruchamianie](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="05a86-154">Wybierz **na** tooenable tych zasad i **poza** toodisable go.</span><span class="sxs-lookup"><span data-stu-id="05a86-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="05a86-155">Po włączeniu tych zasad, określ hello zaplanowany czas rozpoczęcia, strefa czasowa i hello dni tygodnia hello, dla których hello dotyczy czas.</span><span class="sxs-lookup"><span data-stu-id="05a86-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="05a86-156">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="05a86-156">Select **Save**.</span></span>

    <span data-ttu-id="05a86-157">Po włączeniu tych zasad nie jest automatycznie zastosowane tooany maszyn wirtualnych w bieżącym laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="05a86-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="05a86-158">tooapply tooa to ustawienie określonej maszyny Wirtualnej, otwórz hello wirtualna bloku i zmień jego **Auto-start** ustawienie</span><span class="sxs-lookup"><span data-stu-id="05a86-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="05a86-159">Ustawianie daty wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="05a86-159">Set expiration date</span></span>
<span data-ttu-id="05a86-160">Można ustawić wygaśnięcie datę, gdy użytkownik [utworzyć hello wirtualna](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="05a86-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="05a86-161">W **Zaawansowane ustawienia**, wybierz ikonę toospecify kalendarza hello, datę, na którym hello maszyny Wirtualnej zostaną automatycznie usunięte.</span><span class="sxs-lookup"><span data-stu-id="05a86-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="05a86-162">Domyślnie program hello wirtualna nigdy nie wygasa.</span><span class="sxs-lookup"><span data-stu-id="05a86-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="05a86-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05a86-163">Next steps</span></span>
<span data-ttu-id="05a86-164">Po zdefiniowany i zastosować hello różne ustawienia zasad maszyn wirtualnych dla laboratorium, poniżej przedstawiono niektóre czynności tootry obok:</span><span class="sxs-lookup"><span data-stu-id="05a86-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="05a86-165">[Zrozumienie udostępnionego adresy IP](devtest-lab-shared-ip.md) -wyjaśniono, jak udostępnione IP adresy są używane w DevTest Labs toominimize hello liczby laboratorium tooyour tooconnect wymaganych adresów IP publicznego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="05a86-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="05a86-166">[Konfigurowanie kosztów zarządzania](devtest-lab-configure-cost-management.md) -ilustruje sposób toouse hello **miesięczny Trend szacowany koszt** wykresu</span><span class="sxs-lookup"><span data-stu-id="05a86-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="05a86-167">tooview hello bieżącego miesiąca szacowany koszt do daty i hello planowany koszt koniec miesiąca.</span><span class="sxs-lookup"><span data-stu-id="05a86-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="05a86-168">[Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) — podczas tworzenia maszyny Wirtualnej, należy określić podstawowy, który może być niestandardowy obraz lub obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="05a86-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="05a86-169">W tym artykule przedstawiono sposób toocreate niestandardowego obrazu z pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="05a86-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="05a86-170">[Konfigurowanie portalu Marketplace obrazów](devtest-lab-configure-marketplace-images.md) — Azure DevTest Labs obsługuje tworzenie maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="05a86-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="05a86-171">W tym artykule przedstawiono sposób toospecify, którego, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="05a86-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="05a86-172">[Utwórz maszynę Wirtualną w laboratorium](devtest-lab-add-vm-with-artifacts.md) -ilustruje sposób toocreate maszyny Wirtualnej z obrazu podstawowego (albo niestandardowe lub Marketplace) i w jaki sposób toowork z artefaktami w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05a86-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

