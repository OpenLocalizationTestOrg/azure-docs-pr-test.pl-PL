---
title: "Automatyczne skalowanie usługi w chmurze w portalu klasycznym | Dokumentacja firmy Microsoft"
description: "(klasyczne) Dowiedz się, jak skonfigurować regułę automatycznego skalowania dla roli sieci web usługi w chmurze lub roli proces roboczy na platformie Azure przy użyciu klasycznego portalu."
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
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="1c4ba-103">Jak skonfigurować automatyczne skalowanie usługi w chmurze w portalu klasycznym</span><span class="sxs-lookup"><span data-stu-id="1c4ba-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c4ba-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1c4ba-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="1c4ba-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1c4ba-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="1c4ba-106">Na stronie skali w klasycznym portalu Azure można skonfigurować ustawienia skalowania automatycznego dla roli sieci web lub roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="1c4ba-107">Alternatywnie można skonfigurować, ręczne skalowanie zamiast opartych na regułach Skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="1c4ba-108">Ten artykuł dotyczy usługi w chmurze role sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="1c4ba-109">Po utworzeniu maszyny wirtualnej (klasyczne) bezpośrednio, znajduje się w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="1c4ba-110">Niektóre z tych informacji ma zastosowanie do tych typów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="1c4ba-111">Skalowanie zestawu dostępności maszyn wirtualnych jest po prostu wyłączając je włączane i wyłączane na podstawie reguł skalowania, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="1c4ba-112">Aby uzyskać więcej informacji o maszynach wirtualnych i zestawów dostępności, zobacz [Zarządzanie dostępność maszyn wirtualnych](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1c4ba-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="1c4ba-113">Przed skonfigurowaniem skalowania dla aplikacji, należy rozważyć następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1c4ba-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="1c4ba-114">Skalowanie jest zagrożony użycia rdzeni.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="1c4ba-115">Większe wystąpień roli za pomocą większej liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-115">Larger role instances use more cores.</span></span> <span data-ttu-id="1c4ba-116">Można skalować aplikacji tylko w ramach limitu rdzeni dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="1c4ba-117">Na przykład załóżmy, że w subskrypcji ma limit liczby rdzeni (20).</span><span class="sxs-lookup"><span data-stu-id="1c4ba-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="1c4ba-118">Po uruchomieniu aplikacji z dwie średnich chmury usługi (łącznie 4 rdzenie) można tylko zwiększać innych wdrożeń usługi w chmurze w ramach subskrypcji przez pozostałe 16 rdzeni.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="1c4ba-119">Aby uzyskać więcej informacji na temat rozmiarów, zobacz [rozmiary usługi w chmurze](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="1c4ba-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="1c4ba-120">Należy utworzyć kolejkę i skojarzyć go z roli, zanim można skalować aplikacji opartej na próg komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="1c4ba-121">Aby uzyskać więcej informacji, zobacz [sposobu korzystania z usługi magazynowania kolejki](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1c4ba-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="1c4ba-122">Możesz skalować zasoby, które są połączone z usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="1c4ba-123">Aby uzyskać więcej informacji o łączeniu zasobów, zobacz [porady: łączenie zasobu usługi w chmurze](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="1c4ba-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="1c4ba-124">Aby włączyć wysoką dostępność aplikacji, należy upewnić się, że jest wdrażany z dwóch lub więcej wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="1c4ba-125">Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="1c4ba-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="1c4ba-126">Skalowanie harmonogramu</span><span class="sxs-lookup"><span data-stu-id="1c4ba-126">Schedule scaling</span></span>
<span data-ttu-id="1c4ba-127">Domyślnie wszystkie role nie postępuj zgodnie z określonym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="1c4ba-128">W związku z tym zmienić ustawienia dotyczą wszystkie dni i godziny wszystkich przez cały rok.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="1c4ba-129">Jeśli chcesz, możesz skonfigurować ręczne lub automatyczne skalowanie dla jednego z następujących trybów:</span><span class="sxs-lookup"><span data-stu-id="1c4ba-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="1c4ba-130">Dni tygodnia</span><span class="sxs-lookup"><span data-stu-id="1c4ba-130">Weekdays</span></span>
* <span data-ttu-id="1c4ba-131">Weekendy</span><span class="sxs-lookup"><span data-stu-id="1c4ba-131">Weekends</span></span>
* <span data-ttu-id="1c4ba-132">Nocy tygodnia</span><span class="sxs-lookup"><span data-stu-id="1c4ba-132">Week nights</span></span>
* <span data-ttu-id="1c4ba-133">Mornings tygodnia</span><span class="sxs-lookup"><span data-stu-id="1c4ba-133">Week mornings</span></span>
* <span data-ttu-id="1c4ba-134">Konkretne daty</span><span class="sxs-lookup"><span data-stu-id="1c4ba-134">Specific dates</span></span>
* <span data-ttu-id="1c4ba-135">Zakresy określonej daty</span><span class="sxs-lookup"><span data-stu-id="1c4ba-135">Specific date ranges</span></span>

<span data-ttu-id="1c4ba-136">Ustawienia harmonogramu jest skonfigurowany w [klasycznego portalu Azure](https://manage.windowsazure.com/) na</span><span class="sxs-lookup"><span data-stu-id="1c4ba-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="1c4ba-137">**Usługi w chmurze** > **\[usługi w chmurze\]** > **skali** > **\[środowisko produkcyjne lub tymczasowe\]**  strony.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="1c4ba-138">Kliknij przycisk **Konfigurowanie uruchomień** przycisk dla każdej roli, które chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Automatyczne skalowanie usługi chmury zgodnie z harmonogramem][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="1c4ba-140">Ręczne skali</span><span class="sxs-lookup"><span data-stu-id="1c4ba-140">Manual scale</span></span>
<span data-ttu-id="1c4ba-141">Na **skali** strony, można ręcznie zwiększyć lub zmniejszyć liczbę uruchomionych wystąpień w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="1c4ba-142">To ustawienie jest skonfigurowane do każdej harmonogram, który został utworzony lub cały czas, jeśli nie utworzono harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="1c4ba-143">W [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę usługi w chmurze, aby otworzyć pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1c4ba-144">Jeśli nie widzisz usługi w chmurze, może być konieczna zmiana z **produkcji** do **przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="1c4ba-145">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-145">Click **Scale**.</span></span>
3. <span data-ttu-id="1c4ba-146">Wybierz harmonogram, aby zmienić opcje skalowania.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="1c4ba-147">*Nie określonych godzinach* jest wartością domyślną, jeśli masz Brak zdefiniowanych harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="1c4ba-148">Znajdź **skali według metryki** a następnie wybierz opcję **Brak**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="1c4ba-149">To ustawienie jest ustawieniem domyślnym dla wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="1c4ba-150">Każda rola w usłudze w chmurze ma suwak do zmiany liczby wystąpień do użycia.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Ręcznie skalować roli usługi chmury][manual_scale]
   
    <span data-ttu-id="1c4ba-152">Jeśli potrzebujesz więcej wystąpień, może być konieczna zmiana [rozmiar maszyny wirtualnej usługi w chmurze](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="1c4ba-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="1c4ba-153">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-153">Click **Save**.</span></span>  
   <span data-ttu-id="1c4ba-154">Wystąpienia roli są dodawane lub usuwane w oparciu o wybrane opcje.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="1c4ba-155">Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przesuń wskaźnik myszy do niego i można uzyskać pomoc dotyczącą ustawienie określone.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="1c4ba-156">Automatyczne skalowanie - Procesora</span><span class="sxs-lookup"><span data-stu-id="1c4ba-156">Automatic scale - CPU</span></span>
<span data-ttu-id="1c4ba-157">Ten tryb skaluje, jeśli nie jest średnią wartość procentową wykorzystania Procesora powyżej lub poniżej określonej wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="1c4ba-158">Wystąpienia roli są tworzone lub usuwane w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="1c4ba-159">W [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę usługi w chmurze, aby otworzyć pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1c4ba-160">Jeśli nie widzisz usługi w chmurze, może być konieczna zmiana z **produkcji** do **przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="1c4ba-161">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-161">Click **Scale**.</span></span>
3. <span data-ttu-id="1c4ba-162">Wybierz harmonogram, aby zmienić opcje skalowania.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="1c4ba-163">*Nie określonych godzinach* jest wartością domyślną, jeśli masz Brak zdefiniowanych harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="1c4ba-164">Znajdź **skali według metryki** a następnie wybierz opcję **Procesora**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="1c4ba-165">Teraz można skonfigurować minimalną i maksymalną zakresu wystąpień ról, docelowego użycia procesora CPU (w celu wyzwolenia skali w górę) oraz liczbę wystąpień skalowanie w górę i w dół przez.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Skalowanie roli usługi chmury, obciążenie procesora cpu][cpu_scale]

> [!TIP]
> <span data-ttu-id="1c4ba-167">Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przesuń wskaźnik myszy do niego i można uzyskać pomoc dotyczącą ustawienie określone.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="1c4ba-168">Automatyczne skalowanie - kolejki</span><span class="sxs-lookup"><span data-stu-id="1c4ba-168">Automatic scale - Queue</span></span>
<span data-ttu-id="1c4ba-169">Ten tryb jest automatycznie skalowany Jeśli liczba wiadomości w kolejce powyżej lub poniżej określonego progu.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="1c4ba-170">Wystąpienia roli są tworzone lub usuwane w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="1c4ba-171">W [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę usługi w chmurze, aby otworzyć pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1c4ba-172">Jeśli nie widzisz usługi w chmurze, może być konieczna zmiana z **produkcji** do **przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="1c4ba-173">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-173">Click **Scale**.</span></span>
3. <span data-ttu-id="1c4ba-174">Znajdź **skali według metryki** a następnie wybierz opcję **kolejki**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="1c4ba-175">Teraz można skonfigurować minimalną i maksymalną zakresu wystąpień ról, kolejki i liczbę wiadomości w kolejce do przetworzenia dla każdego wystąpienia i skalowanie w górę i w dół, jak wiele wystąpień.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Skalowanie roli usługi chmury, kolejki komunikatów][queue_scale]

> [!TIP]
> <span data-ttu-id="1c4ba-177">Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przesuń wskaźnik myszy do niego i można uzyskać pomoc dotyczącą ustawienie określone.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="1c4ba-178">Skalowanie połączonych zasobów</span><span class="sxs-lookup"><span data-stu-id="1c4ba-178">Scale linked resources</span></span>
<span data-ttu-id="1c4ba-179">Często zdarza się skalowanie roli jest korzystne można skalować bazy danych, który także używa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="1c4ba-180">Jeśli bazy danych do usługi w chmurze, aby dostęp do ustawień dla tego zasobu, kliknąć odpowiednie łącze.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="1c4ba-181">W [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę usługi w chmurze, aby otworzyć pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1c4ba-182">Jeśli nie widzisz usługi w chmurze, może być konieczna zmiana z **produkcji** do **przemieszczania** lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="1c4ba-183">Kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-183">Click **Scale**.</span></span>
3. <span data-ttu-id="1c4ba-184">Znajdź **połączone zasobów** sekcji, a następnie kliknij przycisk **Zarządzaj skalowania dla tej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1c4ba-185">Jeśli nie widzisz **połączone zasobów** sekcji, prawdopodobnie nie masz żadnych połączonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="1c4ba-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
