---
title: "Wdrażanie usługi Azure API Management na wiele regionów platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć wystąpienia usługi Azure API Management na wiele regionów platformy Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="c1ec3-103">Jak wdrożyć wystąpienia usługi Azure API Management na wiele regionów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c1ec3-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="c1ec3-104">Zarządzanie interfejsami API obsługuje wdrażanie w przypadku, dzięki czemu wydawcy interfejsu API rozpowszechniają jednej usługi interfejsu API zarządzania dowolną liczbę żądaną regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="c1ec3-105">Pozwala to zmniejszyć żądania opóźnienia postrzegane przez rozproszone geograficznie konsumentów interfejsu API i zwiększa również dostępność usługi, jeśli jeden region przejdzie do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="c1ec3-106">Podczas tworzenia usługi Zarządzanie interfejsami API w początkowo zawiera tylko jeden [jednostki] [ unit] znajdują się w pojedynczym regionie Azure, który jest wybrany jako regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="c1ec3-107">Dodatkowe regiony można łatwo dodawać za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="c1ec3-108">Zarządzanie interfejsami API serwer bramy jest wdrażany do każdego regionu i ruchu połączenia będą kierowane do najbliższego bramy.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="c1ec3-109">Jeśli region przejdzie do trybu offline, ruch jest automatycznie skierowana do następnego najbliższego bramy.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c1ec3-110">W przypadku wdrażania jest dostępna tylko w  **[Premium] [ Premium]**  warstwy.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="c1ec3-111"><a name="add-region"></a>Wdrożyć nowy region wystąpienia usługi Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="c1ec3-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="c1ec3-112">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c1ec3-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c1ec3-113">W portalu Azure przejdź do **skali i cenach** strony wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Kartę Skala][api-management-scale-service]

<span data-ttu-id="c1ec3-115">Aby wdrożyć nowy region, kliknij polecenie **+ Dodaj region** z paska narzędzi.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Dodawanie regionu][api-management-add-region]

<span data-ttu-id="c1ec3-117">Wybierz lokalizację z listy rozwijanej i ustaw liczbę jednostek dla suwaka.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Określ jednostki][api-management-select-location-units]

<span data-ttu-id="c1ec3-119">Kliknij przycisk **Dodaj** można umieścić w tabeli Lokalizacje wybór.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="c1ec3-120">Powtórz ten proces, dopóki nie uzyskasz wszystkich skonfigurowanych lokalizacji, a następnie kliknij przycisk **zapisać** z paska narzędzi do rozpoczęcia procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="c1ec3-121"><a name="remove-region"></a>Usunąć wystąpienie usługi API Management z lokalizacji</span><span class="sxs-lookup"><span data-stu-id="c1ec3-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="c1ec3-122">W portalu Azure przejdź do **skali i cenach** strony wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Kartę Skala][api-management-scale-service]

<span data-ttu-id="c1ec3-124">Dla lokalizacji, które chcesz usunąć Otwórz za pomocą menu kontekstowego **...**  przycisk na prawym końcu tabeli.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="c1ec3-125">Wybierz **usunąć** opcji.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-125">Select the **Delete** option.</span></span>

![Usuń region][api-management-remove-region]

<span data-ttu-id="c1ec3-127">Potwierdzenie usunięcia, a następnie kliknij przycisk **zapisać** Aby zastosować zmiany.</span><span class="sxs-lookup"><span data-stu-id="c1ec3-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

