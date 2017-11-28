---
title: "aaaAuto skalowania usługi w chmurze w portalu hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello reguł skalowania automatycznego tooconfigure portalu dla roli sieci web usługi w chmurze lub roli proces roboczy na platformie Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="e830a-103">W jaki sposób tooconfigure automatyczne skalowanie usługi w chmurze w portalu hello</span><span class="sxs-lookup"><span data-stu-id="e830a-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e830a-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e830a-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="e830a-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e830a-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="e830a-106">Warunki można ustawić dla roli proces roboczy usługi chmury, wyzwalające skali przychodzący lub wychodzący operacji.</span><span class="sxs-lookup"><span data-stu-id="e830a-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="e830a-107">warunki Hello hello roli może być oparta na powitania Procesora, dysku lub obciążenia sieciowego hello roli.</span><span class="sxs-lookup"><span data-stu-id="e830a-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="e830a-108">Można również ustawić warunek w oparciu metryki komunikat kolejki lub hello z innego zasobu platformy Azure skojarzonych z Twoją subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="e830a-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e830a-109">Ten artykuł dotyczy usługi w chmurze role sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="e830a-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="e830a-110">Po utworzeniu maszyny wirtualnej (klasyczne) bezpośrednio, znajduje się w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e830a-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="e830a-111">Standardowa maszyny wirtualnej można skalować przez skojarzenie jej z [zestawu dostępności](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) i ręcznie włączyć je lub wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="e830a-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="e830a-112">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="e830a-112">Considerations</span></span>
<span data-ttu-id="e830a-113">Należy rozważyć następujące informacje, przed skonfigurowaniem skalowanie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="e830a-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="e830a-114">Skalowanie jest zagrożony użycia rdzeni.</span><span class="sxs-lookup"><span data-stu-id="e830a-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="e830a-115">Większe wystąpień roli za pomocą większej liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="e830a-115">Larger role instances use more cores.</span></span> <span data-ttu-id="e830a-116">Można skalować aplikacji tylko przed upływem limitu hello rdzeni dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e830a-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="e830a-117">Na przykład załóżmy, że w subskrypcji ma limit liczby rdzeni (20).</span><span class="sxs-lookup"><span data-stu-id="e830a-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="e830a-118">Po uruchomieniu aplikacji z dwie średnich chmury usługi (łącznie 4 rdzenie) można tylko zwiększać innych wdrożeń usługi w chmurze w ramach subskrypcji przez hello pozostałe 16 rdzeni.</span><span class="sxs-lookup"><span data-stu-id="e830a-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="e830a-119">Aby uzyskać więcej informacji na temat rozmiarów, zobacz [rozmiary usługi w chmurze](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="e830a-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="e830a-120">Możesz skalować oparte na próg komunikat kolejki.</span><span class="sxs-lookup"><span data-stu-id="e830a-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="e830a-121">Aby uzyskać więcej informacji o tym, jak kolejki toouse, zobacz [jak toouse hello usługi magazynu kolejek](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="e830a-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="e830a-122">Można również skalować innych zasobów skojarzonych z Twoją subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="e830a-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="e830a-123">tooenable wysoką dostępność aplikacji, należy upewnić się, że jest wdrażany z dwóch lub więcej wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="e830a-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="e830a-124">Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="e830a-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="e830a-125">Gdzie znajduje się skali</span><span class="sxs-lookup"><span data-stu-id="e830a-125">Where scale is located</span></span>
<span data-ttu-id="e830a-126">Po wybraniu usługi w chmurze powinny być widoczne bloku usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="e830a-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="e830a-127">W bloku usługi chmury hello, na powitania **ról i wystąpień** kafelka, wybierz hello nazwę hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e830a-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="e830a-128">**WAŻNE**: Upewnij się, że chmura hello tooclick usługi roli, nie hello wystąpienia roli, który znajduje się poniżej roli hello.</span><span class="sxs-lookup"><span data-stu-id="e830a-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="e830a-129">Wybierz hello **skali** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e830a-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="e830a-130">Automatyczne skalowanie</span><span class="sxs-lookup"><span data-stu-id="e830a-130">Automatic scale</span></span>
<span data-ttu-id="e830a-131">Można skonfigurować ustawienia skalowania dla roli, albo w dwóch trybach **ręczne** lub **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="e830a-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="e830a-132">Ręczne zgodnie z regułami, ustaw hello bezwzględną liczbę wystąpień.</span><span class="sxs-lookup"><span data-stu-id="e830a-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="e830a-133">Automatyczne umożliwia jednak tooset, które powinny być skalowane reguły, które kontrolują sposób oraz jak dużo można.</span><span class="sxs-lookup"><span data-stu-id="e830a-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="e830a-134">Zestaw hello **skalowanie przez** opcję zbyt**reguły wydajności i harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="e830a-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Ustawienia skalowania usługi chmury z profilu i reguł](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="e830a-136">Istniejący profil.</span><span class="sxs-lookup"><span data-stu-id="e830a-136">An existing profile.</span></span>
2. <span data-ttu-id="e830a-137">Dodaj regułę hello nadrzędnego profilu.</span><span class="sxs-lookup"><span data-stu-id="e830a-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="e830a-138">Dodaj inny profil.</span><span class="sxs-lookup"><span data-stu-id="e830a-138">Add another profile.</span></span>

<span data-ttu-id="e830a-139">Wybierz **Dodaj profil**.</span><span class="sxs-lookup"><span data-stu-id="e830a-139">Select **Add Profile**.</span></span> <span data-ttu-id="e830a-140">Hello profil określa tryb, który ma być toouse skali hello: **zawsze**, **cyklu**, **Stała data**.</span><span class="sxs-lookup"><span data-stu-id="e830a-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="e830a-141">Po skonfigurowaniu profilu hello i reguły wybierz hello **zapisać** ikona u góry hello.</span><span class="sxs-lookup"><span data-stu-id="e830a-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="e830a-142">Profil</span><span class="sxs-lookup"><span data-stu-id="e830a-142">Profile</span></span>
<span data-ttu-id="e830a-143">profilu Hello Ustawia minimalną i maksymalna liczba wystąpień dla hello skalowania, a także, gdy jest aktywny tego zakresu skali.</span><span class="sxs-lookup"><span data-stu-id="e830a-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="e830a-144">**Zawsze**</span><span class="sxs-lookup"><span data-stu-id="e830a-144">**Always**</span></span>

    <span data-ttu-id="e830a-145">Zawsze Zachowuj ten zakres dostępnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="e830a-145">Always keep this range of instances available.</span></span>  

    ![Usługi w chmurze, która zawsze skalowania](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="e830a-147">**Cyklu**</span><span class="sxs-lookup"><span data-stu-id="e830a-147">**Recurrence**</span></span>

    <span data-ttu-id="e830a-148">Wybierz zestaw dni hello tooscale tygodnia.</span><span class="sxs-lookup"><span data-stu-id="e830a-148">Choose a set of days of hello week tooscale.</span></span>

    ![Skali usługi chmury, za pomocą harmonogramu cyklu](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="e830a-150">**Daty stałej**</span><span class="sxs-lookup"><span data-stu-id="e830a-150">**Fixed Date**</span></span>

    <span data-ttu-id="e830a-151">Rola hello tooscale zakres daty stałej.</span><span class="sxs-lookup"><span data-stu-id="e830a-151">A fixed date range tooscale hello role.</span></span>

    ![Skali usługi chmury z datą stałej](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="e830a-153">Po skonfigurowaniu profilu hello wybierz hello **OK** u dołu hello hello blok profilu.</span><span class="sxs-lookup"><span data-stu-id="e830a-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="e830a-154">Reguła</span><span class="sxs-lookup"><span data-stu-id="e830a-154">Rule</span></span>
<span data-ttu-id="e830a-155">Reguły są dodawane tooa profilu i stanowią warunek wyzwalający hello skali.</span><span class="sxs-lookup"><span data-stu-id="e830a-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="e830a-156">wyzwalacz reguły Hello jest oparta na metryki usługi w chmurze hello (użycie procesora CPU, aktywności dysku lub działanie sieci) toowhich można dodać wartość warunkowego.</span><span class="sxs-lookup"><span data-stu-id="e830a-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="e830a-157">Ponadto można mieć wyzwalacza hello w oparciu metryki komunikat kolejki lub hello z innego zasobu platformy Azure skojarzonych z Twoją subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="e830a-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="e830a-158">Po skonfigurowaniu reguły hello wybierz hello **OK** przycisk u dołu hello hello reguły bloku.</span><span class="sxs-lookup"><span data-stu-id="e830a-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="e830a-159">Utwórz kopię toomanual skali</span><span class="sxs-lookup"><span data-stu-id="e830a-159">Back toomanual scale</span></span>
<span data-ttu-id="e830a-160">Przejdź toohello [ustawień skalowania](#where-scale-is-located) i zestaw hello **skalowanie przez** opcję zbyt**liczba wystąpień ustawiana ręcznie**.</span><span class="sxs-lookup"><span data-stu-id="e830a-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Ustawienia skalowania usługi chmury z profilu i reguł](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="e830a-162">To ustawienie powoduje usunięcie automatyczne skalowanie z roli hello i, można ustawić liczbę wystąpień hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e830a-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="e830a-163">Witaj opcji skalowania (ręczne lub automatyczne).</span><span class="sxs-lookup"><span data-stu-id="e830a-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="e830a-164">Rola wystąpienia suwaka tooset hello wystąpień tooscale do.</span><span class="sxs-lookup"><span data-stu-id="e830a-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="e830a-165">Wystąpienia hello tooscale roli do.</span><span class="sxs-lookup"><span data-stu-id="e830a-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="e830a-166">Po skonfigurowaniu ustawień skalowania hello wybierz hello **zapisać** ikona u góry hello.</span><span class="sxs-lookup"><span data-stu-id="e830a-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
