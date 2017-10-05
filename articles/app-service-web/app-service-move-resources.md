---
title: "Przenoszenie zasobów aplikacji sieci Web w innej grupie zasobów"
description: "W tym artykule opisano scenariusze, w których można przenosić aplikacje sieci Web i aplikacji usługi z jednej grupy zasobów do innego."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="207e6-103">Przenieś obsługiwane konfiguracje</span><span class="sxs-lookup"><span data-stu-id="207e6-103">Supported Move Configurations</span></span>
<span data-ttu-id="207e6-104">Można przenieść zasobów aplikacji sieci Web platformy Azure przy użyciu [API zasobów Przenieś Menedżera zasobów](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="207e6-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="207e6-105">Aplikacje sieci Web platformy Azure obsługuje obecnie następujące scenariusze przenoszenia:</span><span class="sxs-lookup"><span data-stu-id="207e6-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="207e6-106">Przenieś całą zawartość grupy zasobów (aplikacje sieci web, planów usługi aplikacji i certyfikatów) do innej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="207e6-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="207e6-107">Docelowej grupy zasobów nie może zawierać żadnych zasobów Microsoft.Web w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="207e6-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="207e6-108">Przenieś aplikacje sieci web poszczególnych do innej grupie zasobów, podczas nadal hosting je w ich bieżący plan usługi app service (plan usługi aplikacji pozostaje w starym grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="207e6-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


