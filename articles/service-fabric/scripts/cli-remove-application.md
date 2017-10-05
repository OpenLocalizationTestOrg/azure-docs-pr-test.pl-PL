---
title: "Usługa Azure sieci szkieletowej interfejsu wiersza polecenia skryptu Remove próbki"
description: "Usuń aplikację z klastra usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="d969e-103">Usuń aplikację z klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="d969e-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="d969e-104">Ten przykładowy skrypt usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług, wyrejestrowuje typ i wersja aplikacji z klastra.</span><span class="sxs-lookup"><span data-stu-id="d969e-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="d969e-105">Usuwanie wystąpienia aplikacji spowoduje również usunięcie wszystkich uruchomionych wystąpień skojarzoną z daną aplikacją usługi.</span><span class="sxs-lookup"><span data-stu-id="d969e-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="d969e-106">Następnie pliki aplikacji są usuwane z magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="d969e-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="d969e-107">Jeśli to konieczne, zainstaluj [interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d969e-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="d969e-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d969e-108">Sample script</span></span>

<span data-ttu-id="d969e-109">[!code-sh[główne](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "usuwania aplikacji z klastra")]</span><span class="sxs-lookup"><span data-stu-id="d969e-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="d969e-110">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d969e-110">Next steps</span></span>

<span data-ttu-id="d969e-111">Aby uzyskać więcej informacji, zobacz [dokumentacji interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d969e-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="d969e-112">Dodatkowe przykłady interfejsu wiersza polecenia usługi sieci szkieletowej dla sieci szkieletowej usług Azure można znaleźć w [przykłady interfejsu wiersza polecenia usługi sieć szkieletowa](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d969e-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
