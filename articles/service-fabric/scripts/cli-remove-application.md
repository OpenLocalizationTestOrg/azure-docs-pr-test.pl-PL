---
title: "aaaAzure Usuń przykład usługi sieci szkieletowej interfejsu wiersza polecenia skryptu"
description: "Usuń aplikację z klastra usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia Azure Service Fabric hello"
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="a9207-103">Usuń aplikację z klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="a9207-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="a9207-104">Ten przykładowy skrypt usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług, wyrejestrowuje typ i wersja aplikacji z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="a9207-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="a9207-105">Trwa usuwanie wystąpienia aplikacji hello spowoduje również usunięcie hello wszystkie uruchomione wystąpienia usługi skojarzoną z daną aplikacją.</span><span class="sxs-lookup"><span data-stu-id="a9207-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="a9207-106">Następnie pliki aplikacji hello są usuwane z hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="a9207-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="a9207-107">Jeśli to konieczne, zainstaluj hello [interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9207-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="a9207-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a9207-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="a9207-109">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9207-109">Next steps</span></span>

<span data-ttu-id="a9207-110">Aby uzyskać więcej informacji, zobacz hello [dokumentacji interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9207-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="a9207-111">Dodatkowe przykłady interfejsu wiersza polecenia usługi sieci szkieletowej dla sieci szkieletowej usług Azure można znaleźć w hello [przykłady interfejsu wiersza polecenia usługi sieć szkieletowa](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9207-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
