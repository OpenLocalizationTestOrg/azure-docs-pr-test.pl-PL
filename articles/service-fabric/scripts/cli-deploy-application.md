---
title: "aaaAzure przykład usługi sieci szkieletowej interfejsu wiersza polecenia skryptu wdrażania"
description: "Wdrażanie klastra usługi sieć szkieletowa usług Azure tooan dla aplikacji przy użyciu hello Azure Service Fabric interfejsu wiersza polecenia"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="a3c91-103">Wdrażanie klastra usługi sieć szkieletowa tooa aplikacji</span><span class="sxs-lookup"><span data-stu-id="a3c91-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="a3c91-104">Ten przykładowy skrypt kopiuje pakiet tooa klastra obrazu sklepu z aplikacjami, rejestruje typ aplikacji hello w klastrze hello i tworzy wystąpienie aplikacji na podstawie typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a3c91-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="a3c91-105">Wszystkie usługi domyślne są również tworzone w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="a3c91-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="a3c91-106">Jeśli to konieczne, zainstaluj hello [interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a3c91-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="a3c91-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a3c91-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a3c91-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a3c91-108">Clean up deployment</span></span>

<span data-ttu-id="a3c91-109">Po zakończeniu hello [Usuń](cli-remove-application.md) skryptu może być używane tooremove hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3c91-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="a3c91-110">skryptu remove Hello usuwa wystąpienie aplikacji hello wyrejestrowuje typ aplikacji hello i usuwa pakiet aplikacji hello z magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="a3c91-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3c91-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3c91-111">Next steps</span></span>

<span data-ttu-id="a3c91-112">Aby uzyskać więcej informacji, zobacz hello [dokumentacji interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a3c91-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="a3c91-113">Dodatkowe przykłady interfejsu wiersza polecenia usługi sieci szkieletowej dla sieci szkieletowej usług Azure można znaleźć w hello [przykłady interfejsu wiersza polecenia usługi sieć szkieletowa](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a3c91-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
