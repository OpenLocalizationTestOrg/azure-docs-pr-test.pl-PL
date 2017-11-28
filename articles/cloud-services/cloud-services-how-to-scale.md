---
title: "aaaAuto skalowania usługi w chmurze w portalu klasycznym hello | Dokumentacja firmy Microsoft"
description: "(klasyczne) Dowiedz się, jak toouse hello reguł skalowania automatycznego klasycznego portalu tooconfigure dla roli sieci web usługi w chmurze lub roli proces roboczy na platformie Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="7243b-103">W jaki sposób tooconfigure automatyczne skalowanie usługi w chmurze w portalu klasycznym hello</span><span class="sxs-lookup"><span data-stu-id="7243b-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7243b-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7243b-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="7243b-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7243b-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="7243b-106">Na stronie skali hello hello klasycznego portalu Azure można skonfigurować ustawienia skalowania automatycznego dla roli sieci web lub roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="7243b-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="7243b-107">Alternatywnie można skonfigurować, ręczne skalowanie zamiast opartych na regułach Skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="7243b-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="7243b-108">Ten artykuł dotyczy usługi w chmurze role sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="7243b-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="7243b-109">Po utworzeniu maszyny wirtualnej (klasyczne) bezpośrednio, znajduje się w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7243b-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="7243b-110">Niektóre z tych informacji jest stosowana toothese typy maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7243b-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="7243b-111">Skalowanie zestawu dostępności maszyn wirtualnych jest po prostu wyłączając je włączane i wyłączane na podstawie hello skali reguł, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="7243b-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="7243b-112">Aby uzyskać więcej informacji o maszynach wirtualnych i zestawów dostępności, zobacz [hello Zarządzaj dostępność maszyn wirtualnych](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="7243b-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="7243b-113">Należy rozważyć następujące informacje, przed skonfigurowaniem skalowanie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="7243b-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="7243b-114">Skalowanie jest zagrożony użycia rdzeni.</span><span class="sxs-lookup"><span data-stu-id="7243b-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="7243b-115">Większe wystąpień roli za pomocą większej liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="7243b-115">Larger role instances use more cores.</span></span> <span data-ttu-id="7243b-116">Można skalować aplikacji tylko przed upływem limitu hello rdzeni dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7243b-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="7243b-117">Na przykład załóżmy, że w subskrypcji ma limit liczby rdzeni (20).</span><span class="sxs-lookup"><span data-stu-id="7243b-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="7243b-118">Po uruchomieniu aplikacji z dwie średnich chmury usługi (łącznie 4 rdzenie) można tylko zwiększać innych wdrożeń usługi w chmurze w ramach subskrypcji przez hello pozostałe 16 rdzeni.</span><span class="sxs-lookup"><span data-stu-id="7243b-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="7243b-119">Aby uzyskać więcej informacji na temat rozmiarów, zobacz [rozmiary usługi w chmurze](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="7243b-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="7243b-120">Należy utworzyć kolejkę i skojarzyć go z roli, zanim można skalować aplikacji opartej na próg komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7243b-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="7243b-121">Aby uzyskać więcej informacji, zobacz [jak toouse hello usługi magazynu kolejek](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="7243b-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="7243b-122">Zasoby, które są połączone tooyour można skalować usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7243b-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="7243b-123">Aby uzyskać więcej informacji o łączeniu zasobów, zobacz [porady: łączenie usługi w chmurze tooa zasobów](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7243b-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="7243b-124">tooenable wysoką dostępność aplikacji, należy upewnić się, że jest wdrażany z dwóch lub więcej wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="7243b-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="7243b-125">Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="7243b-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="7243b-126">Skalowanie harmonogramu</span><span class="sxs-lookup"><span data-stu-id="7243b-126">Schedule scaling</span></span>
<span data-ttu-id="7243b-127">Domyślnie wszystkie role nie postępuj zgodnie z określonym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="7243b-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="7243b-128">W związku z tym wszystkie ustawienia zmienić się razy tooall oraz wszystkie dni w roku hello.</span><span class="sxs-lookup"><span data-stu-id="7243b-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="7243b-129">Jeśli chcesz, możesz skonfigurować ręczne lub automatyczne skalowanie dla jednego z następujących trybów hello:</span><span class="sxs-lookup"><span data-stu-id="7243b-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="7243b-130">Dni tygodnia</span><span class="sxs-lookup"><span data-stu-id="7243b-130">Weekdays</span></span>
* <span data-ttu-id="7243b-131">Weekendy</span><span class="sxs-lookup"><span data-stu-id="7243b-131">Weekends</span></span>
* <span data-ttu-id="7243b-132">Nocy tygodnia</span><span class="sxs-lookup"><span data-stu-id="7243b-132">Week nights</span></span>
* <span data-ttu-id="7243b-133">Mornings tygodnia</span><span class="sxs-lookup"><span data-stu-id="7243b-133">Week mornings</span></span>
* <span data-ttu-id="7243b-134">Konkretne daty</span><span class="sxs-lookup"><span data-stu-id="7243b-134">Specific dates</span></span>
* <span data-ttu-id="7243b-135">Zakresy określonej daty</span><span class="sxs-lookup"><span data-stu-id="7243b-135">Specific date ranges</span></span>

<span data-ttu-id="7243b-136">Witaj ustawienia harmonogramu jest skonfigurowany w hello [klasycznego portalu Azure](https://manage.windowsazure.com/) na powitania</span><span class="sxs-lookup"><span data-stu-id="7243b-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="7243b-137">**Usługi w chmurze** > **\[usługi w chmurze\]** > **skali** > **\[środowisko produkcyjne lub tymczasowe\]**  strony.</span><span class="sxs-lookup"><span data-stu-id="7243b-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="7243b-138">Kliknij przycisk hello **Konfigurowanie uruchomień** przycisk dla każdej roli ma toochange.</span><span class="sxs-lookup"><span data-stu-id="7243b-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Automatyczne skalowanie usługi chmury zgodnie z harmonogramem][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="7243b-140">Ręczne skali</span><span class="sxs-lookup"><span data-stu-id="7243b-140">Manual scale</span></span>
<span data-ttu-id="7243b-141">Na powitania **skali** strony, można ręcznie zwiększyć lub zmniejszyć liczbę hello uruchomionych wystąpień w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7243b-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="7243b-142">To ustawienie jest skonfigurowane dla każdego harmonogram, który został utworzony lub tooall czasu, jeśli nie utworzono harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="7243b-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="7243b-143">W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="7243b-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7243b-144">Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="7243b-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="7243b-145">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="7243b-145">Click **Scale**.</span></span>
3. <span data-ttu-id="7243b-146">Wybierz harmonogram hello ma toochange opcje do skalowania.</span><span class="sxs-lookup"><span data-stu-id="7243b-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="7243b-147">*Nie określonych godzinach* jest hello domyślną, jeśli masz Brak zdefiniowanych harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="7243b-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="7243b-148">Znajdź hello **skali według metryki** a następnie wybierz opcję **Brak**.</span><span class="sxs-lookup"><span data-stu-id="7243b-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="7243b-149">To ustawienie jest hello domyślnego dla wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="7243b-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="7243b-150">Każda rola hello w usłudze w chmurze ma suwak do zmiany numer hello toouse wystąpień.</span><span class="sxs-lookup"><span data-stu-id="7243b-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Ręcznie skalować roli usługi chmury][manual_scale]
   
    <span data-ttu-id="7243b-152">Jeśli potrzebujesz więcej wystąpień, może być konieczne toochange hello [rozmiar maszyny wirtualnej usługi w chmurze](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="7243b-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="7243b-153">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7243b-153">Click **Save**.</span></span>  
   <span data-ttu-id="7243b-154">Wystąpienia roli są dodawane lub usuwane w oparciu o wybrane opcje.</span><span class="sxs-lookup"><span data-stu-id="7243b-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="7243b-155">Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przenieś tooit Twojego myszy i można uzyskać pomoc dotyczącą ustawienie określone.</span><span class="sxs-lookup"><span data-stu-id="7243b-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="7243b-156">Automatyczne skalowanie - Procesora</span><span class="sxs-lookup"><span data-stu-id="7243b-156">Automatic scale - CPU</span></span>
<span data-ttu-id="7243b-157">W tym trybie skaluje Jeśli hello średnią wartość procentową wykorzystania Procesora powyżej lub poniżej określonej wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="7243b-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="7243b-158">Wystąpienia roli są tworzone lub usuwane w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="7243b-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="7243b-159">W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="7243b-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7243b-160">Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="7243b-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="7243b-161">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="7243b-161">Click **Scale**.</span></span>
3. <span data-ttu-id="7243b-162">Wybierz harmonogram hello ma toochange opcje do skalowania.</span><span class="sxs-lookup"><span data-stu-id="7243b-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="7243b-163">*Nie określonych godzinach* jest hello domyślną, jeśli masz Brak zdefiniowanych harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="7243b-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="7243b-164">Znajdź hello **skali według metryki** a następnie wybierz opcję **Procesora**.</span><span class="sxs-lookup"><span data-stu-id="7243b-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="7243b-165">Teraz można skonfigurować minimalną i maksymalną zakresu wystąpień ról, użycia Procesora docelowy hello (tootrigger a skalowania w górę) oraz liczbę wystąpień tooscale górę i w dół przez.</span><span class="sxs-lookup"><span data-stu-id="7243b-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Skalowanie roli usługi chmury, obciążenie procesora cpu][cpu_scale]

> [!TIP]
> <span data-ttu-id="7243b-167">Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przenieś tooit Twojego myszy i można uzyskać pomoc dotyczącą ustawienie określone.</span><span class="sxs-lookup"><span data-stu-id="7243b-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="7243b-168">Automatyczne skalowanie - kolejki</span><span class="sxs-lookup"><span data-stu-id="7243b-168">Automatic scale - Queue</span></span>
<span data-ttu-id="7243b-169">Ten tryb jest automatycznie skalowany Jeśli hello liczbę wiadomości w kolejce powyżej lub poniżej określonego progu.</span><span class="sxs-lookup"><span data-stu-id="7243b-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="7243b-170">Wystąpienia roli są tworzone lub usuwane w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="7243b-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="7243b-171">W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="7243b-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7243b-172">Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="7243b-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="7243b-173">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="7243b-173">Click **Scale**.</span></span>
3. <span data-ttu-id="7243b-174">Znajdź hello **skali według metryki** a następnie wybierz opcję **kolejki**.</span><span class="sxs-lookup"><span data-stu-id="7243b-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="7243b-175">Teraz można skonfigurować minimalną i maksymalną zakresu wystąpień ról, kolejka hello i liczba kolejki wiadomości tooprocess dla każdego wystąpienia i ile tooscale wystąpień w górę i w dół przez.</span><span class="sxs-lookup"><span data-stu-id="7243b-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Skalowanie roli usługi chmury, kolejki komunikatów][queue_scale]

> [!TIP]
> <span data-ttu-id="7243b-177">Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przenieś tooit Twojego myszy i można uzyskać pomoc dotyczącą ustawienie określone.</span><span class="sxs-lookup"><span data-stu-id="7243b-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="7243b-178">Skalowanie połączonych zasobów</span><span class="sxs-lookup"><span data-stu-id="7243b-178">Scale linked resources</span></span>
<span data-ttu-id="7243b-179">Często skalowanie roli jest bazy danych hello tooscale korzystne, która aplikacja hello używa również.</span><span class="sxs-lookup"><span data-stu-id="7243b-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="7243b-180">Jeśli link hello usługi w chmurze toohello bazy danych, możesz uzyskać dostęp hello skalowanie ustawień dla tego zasobu, klikając odpowiednie łącze hello.</span><span class="sxs-lookup"><span data-stu-id="7243b-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="7243b-181">W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="7243b-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7243b-182">Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="7243b-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="7243b-183">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="7243b-183">Click **Scale**.</span></span>
3. <span data-ttu-id="7243b-184">Znajdź hello **połączone zasobów** sekcji, a następnie kliknij przycisk **Zarządzaj skalowania dla tej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="7243b-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7243b-185">Jeśli nie widzisz **połączone zasobów** sekcji, prawdopodobnie nie masz żadnych połączonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7243b-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
