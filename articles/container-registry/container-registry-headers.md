---
title: Repozytoria rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft
description: "Jak używać repozytoria rejestru kontenera Azure obrazy usługi Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="9a6a7-103">Repozytoria rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9a6a7-103">Azure container registry repositories</span></span>

<span data-ttu-id="9a6a7-104">Rejestry organizacji IANA kontenera platformy Azure są zgodne z wieloma usługami i orchestrators.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="9a6a7-105">Aby ułatwić śledzenie źródła usługi i agentów, na których jest używane ACR, możemy uruchomiony przy użyciu rozwiązania Docker pole nagłówka w pliku Docker.config.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="9a6a7-106">Wyświetlanie repozytoria w portalu</span><span class="sxs-lookup"><span data-stu-id="9a6a7-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="9a6a7-107">Nagłówki ACR wykonaj format:</span><span class="sxs-lookup"><span data-stu-id="9a6a7-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="9a6a7-108">Chmury: Azure, Azure stosu, lub inne dla instytucji rządowych lub chmury Azure określonego kraju.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="9a6a7-109">Mimo że stosu Azure i dla instytucji rządowych chmury nie są obecnie obsługiwane, ten parametr umożliwia wsparcia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="9a6a7-110">Usługi: Nazwa usługi.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-110">Service: name of the service.</span></span>
* <span data-ttu-id="9a6a7-111">Optionalservicename: opcjonalny parametr dla usług z subservices lub Określ jednostki SKU (przykład: aplikacje sieci web odpowiada/app-service/aplikacje sieci web Azure).</span><span class="sxs-lookup"><span data-stu-id="9a6a7-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="9a6a7-112">Usług partnera i orchestrators zaleca się użycie wartości określonego nagłówka ułatwiające pracę z naszych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="9a6a7-113">Użytkownicy mogą również modyfikować wartości przekazane do nagłówka, jeśli potrzebna jest tak.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="9a6a7-114">Wartości chcemy partnerów ACR na potrzeby wypełnić pole "X-Meta-źródła-Client" są poniżej:</span><span class="sxs-lookup"><span data-stu-id="9a6a7-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="9a6a7-115">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="9a6a7-115">Service Name</span></span>              | <span data-ttu-id="9a6a7-116">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="9a6a7-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="9a6a7-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="9a6a7-117">Azure Container Service</span></span>   | <span data-ttu-id="9a6a7-118">/ compute/azure usługi kontenera platformy Azure —</span><span class="sxs-lookup"><span data-stu-id="9a6a7-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="9a6a7-119">Usługi aplikacji — aplikacje sieci Web</span><span class="sxs-lookup"><span data-stu-id="9a6a7-119">App Service - Web Apps</span></span>    | <span data-ttu-id="9a6a7-120">/ app-service/aplikacje sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="9a6a7-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="9a6a7-121">Usługi aplikacji — aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="9a6a7-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="9a6a7-122">Azure/app-service / — aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="9a6a7-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="9a6a7-123">Batch</span><span class="sxs-lookup"><span data-stu-id="9a6a7-123">Batch</span></span>                     | <span data-ttu-id="9a6a7-124">/ compute/partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="9a6a7-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="9a6a7-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="9a6a7-125">Cloud Console</span></span>             | <span data-ttu-id="9a6a7-126">Azure/chmurze konsoli</span><span class="sxs-lookup"><span data-stu-id="9a6a7-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="9a6a7-127">Funkcje</span><span class="sxs-lookup"><span data-stu-id="9a6a7-127">Functions</span></span>                 | <span data-ttu-id="9a6a7-128">Azure/obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="9a6a7-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="9a6a7-129">Internet rzeczy - Centrum</span><span class="sxs-lookup"><span data-stu-id="9a6a7-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="9a6a7-130">Centrum Azure/iot</span><span class="sxs-lookup"><span data-stu-id="9a6a7-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="9a6a7-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a6a7-131">HDInsight</span></span>                 | <span data-ttu-id="9a6a7-132">hdinsight-Azure/danych</span><span class="sxs-lookup"><span data-stu-id="9a6a7-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="9a6a7-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="9a6a7-133">Jenkins</span></span>                   | <span data-ttu-id="9a6a7-134">Azure/wpięć</span><span class="sxs-lookup"><span data-stu-id="9a6a7-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="9a6a7-135">Usługa Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9a6a7-135">Machine Learning</span></span>          | <span data-ttu-id="9a6a7-136">Azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="9a6a7-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="9a6a7-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9a6a7-137">Service Fabric</span></span>            | <span data-ttu-id="9a6a7-138">/ compute /-sieć szkieletowa usług Azure</span><span class="sxs-lookup"><span data-stu-id="9a6a7-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="9a6a7-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="9a6a7-139">VSTS</span></span>                      | <span data-ttu-id="9a6a7-140">Azure/vsts</span><span class="sxs-lookup"><span data-stu-id="9a6a7-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="9a6a7-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a6a7-141">Next steps</span></span>
[<span data-ttu-id="9a6a7-142">Dowiedz się więcej o rejestrów i obsługiwanych usług i orchestrators</span><span class="sxs-lookup"><span data-stu-id="9a6a7-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
