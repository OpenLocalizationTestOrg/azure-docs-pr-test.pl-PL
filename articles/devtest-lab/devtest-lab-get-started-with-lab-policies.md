---
title: "aaaManage zasady podstawowe laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset niektóre hello podstawowych zasad (ustawienia) dla laboratorium w usłudze DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="1b575-103">Zarządzanie zasadami podstawowe dla laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1b575-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="1b575-104">Azure DevTest Labs umożliwia toocontrol kosztów i zminimalizować odpady w Twojej labs przez Zarządzanie zasadami (ustawienia) dla każdego laboratorium.</span><span class="sxs-lookup"><span data-stu-id="1b575-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="1b575-105">W tym artykule należy Rozpoczynanie pracy z zasadami przez learning, jak tooset dwóch najważniejszych zasad hello — ograniczenie hello liczbę maszyn wirtualnych (VM), które zostały utworzone lub żądane przez pojedynczego użytkownika i Konfigurowanie automatycznego zamykania.</span><span class="sxs-lookup"><span data-stu-id="1b575-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="1b575-106">tooview jak tooset każdych zasad laboratorium, zobacz artykuł hello [Definiowanie zasad laboratorium w usłudze Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1b575-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="1b575-107">Uzyskiwanie dostępu do zasad laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1b575-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="1b575-108">Witaj następujące kroki informacje pomocne przy konfigurowaniu zasad dla laboratorium w usłudze Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="1b575-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="1b575-109">zasady hello tooview (i zmiana) dla laboratorium, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1b575-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="1b575-110">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1b575-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="1b575-111">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="1b575-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="1b575-112">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="1b575-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="1b575-113">Wybierz **konfiguracji i zasadach**.</span><span class="sxs-lookup"><span data-stu-id="1b575-113">Select **Configuration and policies**.</span></span>

    ![Blok ustawień zasad](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="1b575-115">Witaj **konfiguracji i zasadach** blok zawiera menu Ustawienia, które można określić.</span><span class="sxs-lookup"><span data-stu-id="1b575-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="1b575-116">W tym artykule opisano tylko hello ustawienia **maszyn wirtualnych dla użytkownika** i **automatyczne zamykanie**.</span><span class="sxs-lookup"><span data-stu-id="1b575-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="1b575-117">toolearn o hello pozostałych ustawień, zobacz [zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1b575-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="1b575-118">Zestaw maszyn wirtualnych dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="1b575-118">Set virtual machines per user</span></span>
<span data-ttu-id="1b575-119">Witaj zasady dla **maszyn wirtualnych dla użytkownika** pozwala toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b575-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="1b575-120">Jeśli użytkownik próbuje toocreate lub oświadczeń maszyny Wirtualnej, gdy limit użytkowników hello zostaną spełnione, komunikat o błędzie wskazuje powitalne tej maszyny Wirtualnej nie może być utworzone/żądane.</span><span class="sxs-lookup"><span data-stu-id="1b575-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="1b575-121">W laboratorium hello **konfiguracji i zasadach** menu, wybierz opcję **maszyn wirtualnych dla użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1b575-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Maszyny wirtualne na użytkownika](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="1b575-123">Wybierz **tak** toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1b575-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="1b575-124">Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="1b575-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="1b575-125">W przypadku wybrania **tak**, wprowadź wartość liczbową wskazujący hello maksymalną liczbę maszyn wirtualnych, które można utworzyć ani przejęte przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b575-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="1b575-126">Wybierz **tak** toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD (dysk SSD).</span><span class="sxs-lookup"><span data-stu-id="1b575-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="1b575-127">Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="1b575-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="1b575-128">W przypadku wybrania **tak**, wprowadź wartość wskazującą maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przy użyciu dysków SSD hello.</span><span class="sxs-lookup"><span data-stu-id="1b575-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="1b575-129">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1b575-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="1b575-130">Ustaw automatyczne zamykanie</span><span class="sxs-lookup"><span data-stu-id="1b575-130">Set auto-shutdown</span></span>
<span data-ttu-id="1b575-131">zasady automatycznego zamykania Hello pomaga laboratorium toominimize odpady zezwalając czasu hello toospecify, zamykania maszyn wirtualnych w tym laboratorium.</span><span class="sxs-lookup"><span data-stu-id="1b575-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="1b575-132">W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **automatyczne zamykanie**.</span><span class="sxs-lookup"><span data-stu-id="1b575-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Automatyczne zamykanie](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="1b575-134">Wybierz **na** tooenable tych zasad i **poza** toodisable go.</span><span class="sxs-lookup"><span data-stu-id="1b575-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="1b575-135">Po włączeniu tych zasad, należy określić hello tooshut godziny (i strefy czasowej) w dół wszystkich maszyn wirtualnych w bieżącym laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="1b575-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="1b575-136">Określ **tak** lub **nr** dla toosend opcji hello toohello przed 15 minut powiadomień określona czasu automatycznego zamykania.</span><span class="sxs-lookup"><span data-stu-id="1b575-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="1b575-137">Jeśli określisz **tak**, wprowadź powiadomienie hello tooreceive punktu końcowego adresu URL elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1b575-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="1b575-138">Aby uzyskać więcej informacji na temat elementów webhook, zobacz [tworzenia elementu webhook lub funkcja interfejsu API Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="1b575-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="1b575-139">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1b575-139">Select **Save**.</span></span>

    <span data-ttu-id="1b575-140">Domyślnie po włączeniu ta zasada dotyczy maszyn wirtualnych tooall w bieżącym laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="1b575-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="1b575-141">tooremove tego ustawienia z określonej maszyny Wirtualnej, otwórz blok hello maszyny Wirtualnej i zmień jego **automatyczne zamykanie** ustawienie</span><span class="sxs-lookup"><span data-stu-id="1b575-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="1b575-142">Ustaw automatyczne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="1b575-142">Set auto-start</span></span>
<span data-ttu-id="1b575-143">zasady automatycznego uruchamiania Hello umożliwia toospecify hello maszyn wirtualnych w bieżącym laboratorium hello powinna być uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="1b575-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="1b575-144">W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="1b575-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Automatyczne uruchamianie](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="1b575-146">Wybierz **na** tooenable tych zasad i **poza** toodisable go.</span><span class="sxs-lookup"><span data-stu-id="1b575-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="1b575-147">Po włączeniu tych zasad, określ hello zaplanowany czas rozpoczęcia, strefa czasowa i hello dni tygodnia hello, dla których hello dotyczy czas.</span><span class="sxs-lookup"><span data-stu-id="1b575-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="1b575-148">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1b575-148">Select **Save**.</span></span>

    <span data-ttu-id="1b575-149">Po włączeniu tych zasad nie jest automatycznie zastosowane tooany maszyn wirtualnych w bieżącym laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="1b575-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="1b575-150">tooapply tooa to ustawienie określonej maszyny Wirtualnej, otwórz hello wirtualna bloku i zmień jego **Auto-start** ustawienie</span><span class="sxs-lookup"><span data-stu-id="1b575-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1b575-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b575-151">Next steps</span></span>

- <span data-ttu-id="1b575-152">[Definiowanie zasad laboratorium w usłudze Azure DevTest Labs](devtest-lab-set-lab-policy.md) — Dowiedz się, jak toomodify innych zasad laboratorium</span><span class="sxs-lookup"><span data-stu-id="1b575-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
