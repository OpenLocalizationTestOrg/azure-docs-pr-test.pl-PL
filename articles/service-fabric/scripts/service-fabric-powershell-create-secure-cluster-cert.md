---
title: "Skrypt programu PowerShell Azure przykładowe — Tworzenie klastra sieci szkieletowej usług | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="96526-103">Tworzenie klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="96526-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="96526-104">Ten przykładowy skrypt tworzy klaster sieci szkieletowej usług pięcioma węzłami klastra zabezpieczone za pomocą certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="96526-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="96526-105">Polecenie tworzy certyfikat z podpisem własnym i przekazuje go do nowego magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="96526-105">The command creates a self-signed certificate and uploads it to a new key vault.</span></span> <span data-ttu-id="96526-106">Certyfikat jest również kopiowany do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="96526-106">The certificate is also copied to a local directory.</span></span>  <span data-ttu-id="96526-107">Ustaw *-OS* parametr, aby wybrać wersję systemu Windows lub Linux, działającą w węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="96526-107">Set the *-OS* parameter to choose the version of Windows or Linux that runs on the cluster nodes.</span></span>  <span data-ttu-id="96526-108">Dostosuj parametry zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="96526-108">Customize the parameters as needed.</span></span>

<span data-ttu-id="96526-109">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview) , a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="96526-109">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="96526-110">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="96526-110">Sample script</span></span>

<span data-ttu-id="96526-111">[!code-powershell[główne](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Tworzenie klastra sieci szkieletowej usług")]</span><span class="sxs-lookup"><span data-stu-id="96526-111">[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="96526-112">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="96526-112">Clean up deployment</span></span> 

<span data-ttu-id="96526-113">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów klastra i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="96526-113">After the script sample has been run, the following command can be used to remove the resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="96526-114">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="96526-114">Script explanation</span></span>

<span data-ttu-id="96526-115">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="96526-115">This script uses the following commands.</span></span> <span data-ttu-id="96526-116">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="96526-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="96526-117">Polecenie</span><span class="sxs-lookup"><span data-stu-id="96526-117">Command</span></span> | <span data-ttu-id="96526-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="96526-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96526-119">Nowe AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="96526-119">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="96526-120">Tworzy nowy klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="96526-120">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96526-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96526-121">Next steps</span></span>

<span data-ttu-id="96526-122">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96526-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="96526-123">Dodatkowe przykłady programu Azure Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="96526-123">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
