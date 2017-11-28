---
title: repozytoria rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft
description: "Jak toouse magazynach rejestru kontenera Azure obrazy usługi Docker"
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
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="657e8-103">Repozytoria rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="657e8-103">Azure container registry repositories</span></span>

<span data-ttu-id="657e8-104">Rejestry organizacji IANA kontenera platformy Azure są zgodne z wieloma usługami i orchestrators.</span><span class="sxs-lookup"><span data-stu-id="657e8-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="657e8-105">toomake go łatwiejsze tootrack hello źródła usługi i agentów, na których jest używane ACR, możemy uruchomiony przy użyciu pola nagłówka Docker hello w pliku Docker.config hello.</span><span class="sxs-lookup"><span data-stu-id="657e8-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="657e8-106">Wyświetlanie repozytoria w hello portalu</span><span class="sxs-lookup"><span data-stu-id="657e8-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="657e8-107">nagłówki ACR Hello wykonaj hello format:</span><span class="sxs-lookup"><span data-stu-id="657e8-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="657e8-108">Chmury: Azure, Azure stosu, lub inne dla instytucji rządowych lub chmury Azure określonego kraju.</span><span class="sxs-lookup"><span data-stu-id="657e8-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="657e8-109">Mimo że stosu Azure i dla instytucji rządowych chmury nie są obecnie obsługiwane, ten parametr umożliwia wsparcia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="657e8-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="657e8-110">Usługi: Nazwa hello usługi.</span><span class="sxs-lookup"><span data-stu-id="657e8-110">Service: name of hello service.</span></span>
* <span data-ttu-id="657e8-111">Optionalservicename: opcjonalny parametr dla usług z subservices lub toospecify jednostki SKU (przykład: aplikacje sieci web odpowiada/app-service/aplikacje sieci web Azure).</span><span class="sxs-lookup"><span data-stu-id="657e8-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="657e8-112">Partner usługi i orchestrators są zachęcani toouse określonego nagłówka wartości toohelp z naszych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="657e8-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="657e8-113">Użytkownicy, można również zmodyfikować wartość hello przekazanego toohello nagłówka, jeśli potrzebna jest tak.</span><span class="sxs-lookup"><span data-stu-id="657e8-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="657e8-114">chcemy ACR partnerów toouse toopopulate hello "X-Meta-źródła-Client" pole wartości Hello jest poniżej:</span><span class="sxs-lookup"><span data-stu-id="657e8-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="657e8-115">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="657e8-115">Service Name</span></span>              | <span data-ttu-id="657e8-116">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="657e8-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="657e8-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="657e8-117">Azure Container Service</span></span>   | <span data-ttu-id="657e8-118">/ compute/azure usługi kontenera platformy Azure —</span><span class="sxs-lookup"><span data-stu-id="657e8-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="657e8-119">Usługi aplikacji — aplikacje sieci Web</span><span class="sxs-lookup"><span data-stu-id="657e8-119">App Service - Web Apps</span></span>    | <span data-ttu-id="657e8-120">/ app-service/aplikacje sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="657e8-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="657e8-121">Usługi aplikacji — aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="657e8-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="657e8-122">Azure/app-service / — aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="657e8-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="657e8-123">Batch</span><span class="sxs-lookup"><span data-stu-id="657e8-123">Batch</span></span>                     | <span data-ttu-id="657e8-124">/ compute/partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="657e8-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="657e8-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="657e8-125">Cloud Console</span></span>             | <span data-ttu-id="657e8-126">Azure/chmurze konsoli</span><span class="sxs-lookup"><span data-stu-id="657e8-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="657e8-127">Funkcje</span><span class="sxs-lookup"><span data-stu-id="657e8-127">Functions</span></span>                 | <span data-ttu-id="657e8-128">Azure/obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="657e8-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="657e8-129">Internet rzeczy - Centrum</span><span class="sxs-lookup"><span data-stu-id="657e8-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="657e8-130">Centrum Azure/iot</span><span class="sxs-lookup"><span data-stu-id="657e8-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="657e8-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="657e8-131">HDInsight</span></span>                 | <span data-ttu-id="657e8-132">hdinsight-Azure/danych</span><span class="sxs-lookup"><span data-stu-id="657e8-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="657e8-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="657e8-133">Jenkins</span></span>                   | <span data-ttu-id="657e8-134">Azure/wpięć</span><span class="sxs-lookup"><span data-stu-id="657e8-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="657e8-135">Usługa Machine Learning</span><span class="sxs-lookup"><span data-stu-id="657e8-135">Machine Learning</span></span>          | <span data-ttu-id="657e8-136">Azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="657e8-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="657e8-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="657e8-137">Service Fabric</span></span>            | <span data-ttu-id="657e8-138">/ compute /-sieć szkieletowa usług Azure</span><span class="sxs-lookup"><span data-stu-id="657e8-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="657e8-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="657e8-139">VSTS</span></span>                      | <span data-ttu-id="657e8-140">Azure/vsts</span><span class="sxs-lookup"><span data-stu-id="657e8-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="657e8-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="657e8-141">Next steps</span></span>
[<span data-ttu-id="657e8-142">Dowiedz się więcej o rejestrów i hello obsługiwane usługi i orchestrators</span><span class="sxs-lookup"><span data-stu-id="657e8-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
