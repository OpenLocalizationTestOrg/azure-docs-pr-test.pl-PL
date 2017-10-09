---
title: "aaaScale przydziały i limity w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale laboratorium w usłudze Azure DevTest Labs"
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="c6152-103">Skalowanie przydziały i limity w usłudze DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c6152-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="c6152-104">Podczas pracy w usłudze DevTest Labs, można zauważyć, że istnieją pewne domyślne limity toosome zasobów platformy Azure, które mogą mieć wpływ na usługi DevTest Labs hello.</span><span class="sxs-lookup"><span data-stu-id="c6152-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="c6152-105">Te granice są określonego tooas **przydziały**.</span><span class="sxs-lookup"><span data-stu-id="c6152-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="c6152-106">Witaj usługi DevTest Labs nie nakładają żadnych przydziałów.</span><span class="sxs-lookup"><span data-stu-id="c6152-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="c6152-107">Wszelkie przydziałów, które mogą wystąpić są domyślne ograniczenia hello subskrypcji ogólna platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6152-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="c6152-108">Można użyć każdego zasobów platformy Azure, aż dojdziesz limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="c6152-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="c6152-109">Każda subskrypcja ma oddzielne przydziały i użycia są śledzone na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c6152-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="c6152-110">Na przykład każda subskrypcja ma domyślnego przydziału rdzeni 20.</span><span class="sxs-lookup"><span data-stu-id="c6152-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="c6152-111">Dlatego w przypadku tworzenia maszyn wirtualnych w laboratorium z czterech rdzeni, następnie można tworzyć tylko pięć maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c6152-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="c6152-112">[Azure subskrypcji i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits) przedstawiono niektóre z najczęściej przydziały hello zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6152-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="c6152-113">Hello zasoby najczęściej używane w laboratorium, a dla mogą wystąpić przydziałów, zawierają rdzeni maszyny Wirtualnej, publiczne adresy IP interfejsu sieciowego, dysków zarządzanych, przypisanie roli RBAC i obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c6152-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="c6152-114">Wyświetlanie Twoich użycia i przydziały</span><span class="sxs-lookup"><span data-stu-id="c6152-114">View your usage and quotas</span></span>
<span data-ttu-id="c6152-115">Te kroki pokazują, jak tooview hello bieżącego przydziały w subskrypcji dla określonych zasobów platformy Azure i toosee, jaki procent każdego przydziału zostały użyte.</span><span class="sxs-lookup"><span data-stu-id="c6152-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="c6152-116">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c6152-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="c6152-117">Wybierz **więcej usług**, a następnie wybierz **rozliczeń** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="c6152-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="c6152-118">W bloku rozliczenia hello Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c6152-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="c6152-119">Wybierz **użycia + przydziały**.</span><span class="sxs-lookup"><span data-stu-id="c6152-119">Select **Usage + quotas**.</span></span>

   ![Przycisk użycia i przydziały](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="c6152-121">Witaj użycia + przydziały zostanie wyświetlony blok wyświetlania różne zasoby dostępne w tej subskrypcji oraz hello procent przydziału hello, który jest używany dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6152-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Przydziały i użycia](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="c6152-123">Żąda więcej zasobów w Twojej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c6152-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="c6152-124">Przekroczenie limitu przydziału hello domyślny limit zasobów w subskrypcji można zwiększyć się tooa maksymalny limit, zgodnie z opisem w [subskrypcji platformy Azure i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="c6152-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="c6152-125">Te kroki pokazują, jak toorequest, zwiększ limit przydziału, za pośrednictwem hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c6152-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="c6152-126">Wybierz **więcej usług**, wybierz pozycję **rozliczeń**, a następnie wybierz **użycia + przydziały**.</span><span class="sxs-lookup"><span data-stu-id="c6152-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="c6152-127">Witaj użycia + bloku przydziałów, wybierz hello **żądanie zwiększenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6152-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Przycisk Zwiększ żądania](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="c6152-129">toocomplete i przesłać Żądanie hello, wypełnij hello wymagane informacje na wszystkich kartach trzy hello **nowy obsługuje żądania** formularza.</span><span class="sxs-lookup"><span data-stu-id="c6152-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Zwiększ formularz żądania](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="c6152-131">[Opis ograniczeń Azure i zwiększa](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) zawiera więcej informacji o skontaktowaniu się z pomocą techniczną platformy Azure toorequest przydział zwiększenia.</span><span class="sxs-lookup"><span data-stu-id="c6152-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="c6152-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6152-132">Next steps</span></span>
* <span data-ttu-id="c6152-133">Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="c6152-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
