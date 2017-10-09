---
title: "toomultiple Azure usługi Azure API Management aaaDeploy regionów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy Azure API Management usługi toomultiple wystąpienia Azure regionów."
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
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="c08d4-103">Jak toodeploy Azure API Management usługi toomultiple wystąpienia Azure regionów</span><span class="sxs-lookup"><span data-stu-id="c08d4-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="c08d4-104">Zarządzanie interfejsami API obsługuje wdrożenia w przypadku, dzięki czemu interfejsu API wydawców toodistribute pojedynczą usługę zarządzania interfejsu API przez dowolną liczbę żądaną regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c08d4-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="c08d4-105">Pozwala to zmniejszyć żądania opóźnienia postrzegane przez rozproszone geograficznie konsumentów interfejsu API i zwiększa również dostępność usługi, jeśli jeden region przejdzie do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="c08d4-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="c08d4-106">Podczas tworzenia usługi Zarządzanie interfejsami API w początkowo zawiera tylko jeden [jednostki] [ unit] znajdują się w pojedynczym regionie Azure, który jest wybrany jako hello regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="c08d4-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="c08d4-107">Dodatkowe regiony można łatwo dodać za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c08d4-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="c08d4-108">Zarządzanie interfejsami API serwera bramy jest region tooeach wdrożone i ruchu wywołania będzie routingiem toohello najbliższego bramy.</span><span class="sxs-lookup"><span data-stu-id="c08d4-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="c08d4-109">Jeśli region przejdzie do trybu offline, hello jest automatycznie ponownie ukierunkowanej toohello dalej najbliższego bramy.</span><span class="sxs-lookup"><span data-stu-id="c08d4-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c08d4-110">W przypadku wdrażania jest dostępna tylko w hello  **[Premium] [ Premium]**  warstwy.</span><span class="sxs-lookup"><span data-stu-id="c08d4-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="c08d4-111"><a name="add-region"></a>Wdrażanie zarządzanie interfejsami API usługi wystąpienia tooa nowy region</span><span class="sxs-lookup"><span data-stu-id="c08d4-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="c08d4-112">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="c08d4-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c08d4-113">W portalu Azure hello Przejdź toohello **skali i cenach** strony wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="c08d4-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Kartę Skala][api-management-scale-service]

<span data-ttu-id="c08d4-115">toodeploy tooa nowy region, kliknij polecenie **+ Dodaj region** z hello paska narzędzi.</span><span class="sxs-lookup"><span data-stu-id="c08d4-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Dodawanie regionu][api-management-add-region]

<span data-ttu-id="c08d4-117">Wybierz z listy rozwijanej hello hello lokalizacji i ustaw hello liczba jednostek z hello suwaka.</span><span class="sxs-lookup"><span data-stu-id="c08d4-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Określ jednostki][api-management-select-location-units]

<span data-ttu-id="c08d4-119">Kliknij przycisk **Dodaj** tooplace wybór hello lokalizacji tabeli.</span><span class="sxs-lookup"><span data-stu-id="c08d4-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="c08d4-120">Powtórz ten proces, dopóki nie uzyskasz wszystkich skonfigurowanych lokalizacji, a następnie kliknij przycisk **zapisać** z procesu wdrażania hello hello narzędzi toostart.</span><span class="sxs-lookup"><span data-stu-id="c08d4-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="c08d4-121"><a name="remove-region"></a>Usunąć wystąpienie usługi API Management z lokalizacji</span><span class="sxs-lookup"><span data-stu-id="c08d4-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="c08d4-122">W portalu Azure hello Przejdź toohello **skali i cenach** strony wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="c08d4-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Kartę Skala][api-management-scale-service]

<span data-ttu-id="c08d4-124">Dla lokalizacji hello chcesz tooremove Otwórz menu kontekstowe hello przy użyciu hello **...**  przycisku po prawej stronie powitania hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="c08d4-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="c08d4-125">Wybierz hello **usunąć** opcji.</span><span class="sxs-lookup"><span data-stu-id="c08d4-125">Select hello **Delete** option.</span></span>

![Usuń region][api-management-remove-region]

<span data-ttu-id="c08d4-127">Potwierdź usunięcie hello, a następnie kliknij przycisk **zapisać** tooapply hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="c08d4-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

