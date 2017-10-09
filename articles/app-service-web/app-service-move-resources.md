---
title: "aaaMove zasobów aplikacji sieci Web tooanother grupy zasobów"
description: "Opisano scenariusze hello, których można przenosić aplikacje sieci Web i aplikacji usługi z jednym tooanother grupy zasobów."
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
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="27837-103">Przenieś obsługiwane konfiguracje</span><span class="sxs-lookup"><span data-stu-id="27837-103">Supported Move Configurations</span></span>
<span data-ttu-id="27837-104">Można przenieść zasobów aplikacji sieci Web platformy Azure przy użyciu hello [API zasobów Przenieś Menedżera zasobów](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="27837-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="27837-105">Aplikacje sieci Web platformy Azure obsługuje obecnie następujące scenariusze przenoszenia hello:</span><span class="sxs-lookup"><span data-stu-id="27837-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="27837-106">Przenieś hello całą zawartość grupy zasobów (aplikacje sieci web, planów usługi aplikacji i certyfikaty) tooanother grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="27837-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="27837-107">Grupa zasobów Hello docelowego nie może zawierać żadnych zasobów Microsoft.Web w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="27837-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="27837-108">Przenieś poszczególnych sieci web apps tooa innej grupie zasobów, podczas nadal hosting je w ich bieżący plan usługi app service (hello aplikacji usługi plan pozostaje w grupie zasobów starego hello).</span><span class="sxs-lookup"><span data-stu-id="27837-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


