---
title: "Wdrażanie aplikacji w usłudze Azure App Service"
description: "Dowiedz się, jak wdrażanie aplikacji do pracy z usługi aplikacji"
keywords: "usługi aplikacji usługi azure aplikacji, wdrażanie i wdrożenia"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="e8cb3-104">Omówienie wdrażania usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="e8cb3-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="e8cb3-105">Usługa aplikacji Azure oferuje bogaty i zintegrowane funkcję ustawioną obsługują tworzenie przepływów pracy wdrażania wydajny i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="e8cb3-106">Wdrażanie aplikacji, można wykorzystać opcje, takie jak ciągła integracja i kontroli źródła lokalnego publikowania, WebDeploy oraz FTP.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="e8cb3-107">Zalecana metoda wdrażania aplikacji w produkcji jest wymiany miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="e8cb3-108">Miejsca wdrożenia reprezentuje środowisk przemieszczania i integracji skojarzonych z aplikacjami produkcji.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="e8cb3-109">Można konfigurować miejsc wdrożenia i zastosować ruchu w sieci web do sprawdzania poprawności i ruchu może być zamieniona na żądanie dla wdrożenia do środowiska produkcyjnego bez dół czasu i automatyczne zwiększanie gotowości.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="e8cb3-110">Kroki wdrażania przepływu pracy można łatwo zautomatyzować za pomocą wersji produktów zarządzania, takich jak program Visual Studio Release Management.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="e8cb3-111">Jest to przydatne w przypadku koordynacji z innych rozwiązań zasobów (np. Magazyn danych), cyklu i replikacji w wielu jednostkach wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e8cb3-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

