---
title: "aaaAzure przykładowy skrypt programu PowerShell — Tworzenie klastra usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Tworzenie klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="dcd9d-103">Tworzenie klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="dcd9d-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="dcd9d-104">Ten przykładowy skrypt tworzy klaster sieci szkieletowej usług pięcioma węzłami klastra zabezpieczone za pomocą certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="dcd9d-105">polecenie Hello tworzy certyfikat z podpisem własnym i przekazanie jej tooa nowego magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="dcd9d-106">certyfikat Hello jest również skopiowanych tooa katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="dcd9d-107">Zestaw hello *-OS* parametru toochoose hello wersji systemu Windows lub Linux uruchamianego na powitania węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="dcd9d-108">Dostosuj parametry hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="dcd9d-109">Jeśli to konieczne, zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview) , a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dcd9d-110">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="dcd9d-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dcd9d-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="dcd9d-111">Clean up deployment</span></span> 

<span data-ttu-id="dcd9d-112">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów używanych tooremove hello, klastra i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="dcd9d-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="dcd9d-113">Script explanation</span></span>

<span data-ttu-id="dcd9d-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-114">This script uses hello following commands.</span></span> <span data-ttu-id="dcd9d-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dcd9d-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="dcd9d-116">Command</span></span> | <span data-ttu-id="dcd9d-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dcd9d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcd9d-118">Nowe AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="dcd9d-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="dcd9d-119">Tworzy nowy klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dcd9d-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcd9d-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dcd9d-120">Next steps</span></span>

<span data-ttu-id="dcd9d-121">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcd9d-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dcd9d-122">Dodatkowe przykłady programu Azure Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dcd9d-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
