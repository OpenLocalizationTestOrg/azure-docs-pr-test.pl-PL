---
title: "Skalowanie przydziały i limity w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować laboratorium w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="a2957-103">Skalowanie przydziały i limity w usłudze DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a2957-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="a2957-104">Podczas pracy w usłudze DevTest Labs, można zauważyć, że istnieją pewne domyślne limity do niektórych zasobów platformy Azure, co może wpłynąć na usługę DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a2957-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="a2957-105">Ograniczenia te są określane jako **przydziały**.</span><span class="sxs-lookup"><span data-stu-id="a2957-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="a2957-106">Usługa DevTest Labs nie nakładają żadnych przydziałów.</span><span class="sxs-lookup"><span data-stu-id="a2957-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="a2957-107">Wszelkie przydziałów, które mogą wystąpić są domyślne ograniczenia ogólne Azure subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a2957-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="a2957-108">Można użyć każdego zasobów platformy Azure, aż dojdziesz limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="a2957-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="a2957-109">Każda subskrypcja ma oddzielne przydziały i użycia są śledzone na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="a2957-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="a2957-110">Na przykład każda subskrypcja ma domyślnego przydziału rdzeni 20.</span><span class="sxs-lookup"><span data-stu-id="a2957-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="a2957-111">Dlatego w przypadku tworzenia maszyn wirtualnych w laboratorium z czterech rdzeni, następnie można tworzyć tylko pięć maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a2957-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="a2957-112">[Azure subskrypcji i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits) przedstawiono niektóre z najczęściej przydziały dla zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2957-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="a2957-113">Zasoby najczęściej używane w laboratorium, a dla mogą wystąpić przydziały, zawierają rdzeni maszyny Wirtualnej, publiczne adresy IP interfejsu sieciowego, dysków zarządzanych, przypisanie roli RBAC i obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a2957-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="a2957-114">Wyświetlanie Twoich użycia i przydziały</span><span class="sxs-lookup"><span data-stu-id="a2957-114">View your usage and quotas</span></span>
<span data-ttu-id="a2957-115">Te kroki pokazują, jak wyświetlić bieżący przydziały w subskrypcji dla określonych zasobów platformy Azure i zobacz, jaki procent każdego przydziału zostały użyte.</span><span class="sxs-lookup"><span data-stu-id="a2957-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="a2957-116">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a2957-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="a2957-117">Wybierz **więcej usług**, a następnie wybierz **rozliczeń** z listy.</span><span class="sxs-lookup"><span data-stu-id="a2957-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="a2957-118">W bloku rozliczenia Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="a2957-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="a2957-119">Wybierz **użycia + przydziały**.</span><span class="sxs-lookup"><span data-stu-id="a2957-119">Select **Usage + quotas**.</span></span>

   ![Przycisk użycia i przydziały](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="a2957-121">Użycie + przydziały zostanie wyświetlony blok, listę różnych dostępnych zasobów w subskrypcji i procent przydziału, który jest używany dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="a2957-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Przydziały i użycia](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="a2957-123">Żąda więcej zasobów w Twojej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a2957-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="a2957-124">Przekroczenie limitu przydziału domyślny limit zasobów w subskrypcji można zwiększyć maksymalnego limitu, zgodnie z opisem w [subskrypcji platformy Azure i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="a2957-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="a2957-125">Tych krokach przedstawiono sposób zażądać zwiększenia limitu przydziału przez [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a2957-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="a2957-126">Wybierz **więcej usług**, wybierz pozycję **rozliczeń**, a następnie wybierz **użycia + przydziały**.</span><span class="sxs-lookup"><span data-stu-id="a2957-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="a2957-127">Użycie + przydziały bloku, wybierz opcję **żądanie zwiększenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2957-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![Przycisk Zwiększ żądania](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="a2957-129">Aby zakończyć i przesłać żądanie, wypełnij wymagane informacje na wszystkich trzech kartach **nowy obsługuje żądania** formularza.</span><span class="sxs-lookup"><span data-stu-id="a2957-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![Zwiększ formularz żądania](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="a2957-131">[Opis ograniczeń Azure i zwiększa](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) zawiera więcej informacji o skontaktowaniu się z pomocą techniczną platformy Azure, aby zażądać zwiększenia limitu przydziału.</span><span class="sxs-lookup"><span data-stu-id="a2957-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="a2957-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2957-132">Next steps</span></span>
* <span data-ttu-id="a2957-133">Eksploruj [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="a2957-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
