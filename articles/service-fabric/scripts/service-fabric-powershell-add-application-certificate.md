---
title: "aaaAzure przykładowy skrypt programu PowerShell — Dodawanie aplikacji cert tooa klastra | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Dodaj klaster sieci szkieletowej usług tooa aplikacji certyfikatu."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="1bf84-103">Dodaj klaster sieci szkieletowej usług tooa certyfikat aplikacji</span><span class="sxs-lookup"><span data-stu-id="1bf84-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="1bf84-104">Ten przykładowy skrypt tworzy certyfikat z podpisem własnym w hello określonej usługi Azure key vault i instaluje je tooall węzłów klastra usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="1bf84-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="1bf84-105">certyfikat Hello pobiera również tooa folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="1bf84-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="1bf84-106">Hello nazwę certyfikatu pobrane hello jest hello taka sama jak nazwa hello hello certyfikatu w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="1bf84-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="1bf84-107">Dostosuj parametry hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1bf84-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="1bf84-108">Jeśli to konieczne, zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview) , a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf84-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1bf84-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="1bf84-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="1bf84-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="1bf84-110">Script explanation</span></span>

<span data-ttu-id="1bf84-111">Ten skrypt używa hello następującego polecenia: każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1bf84-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1bf84-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="1bf84-112">Command</span></span> | <span data-ttu-id="1bf84-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1bf84-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1bf84-114">Dodaj AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="1bf84-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="1bf84-115">Dodaj wchodzących w skład klastra hello zestawu skalowania maszyn wirtualnych toohello certyfikatu w usłudze nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bf84-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="1bf84-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bf84-116">Next steps</span></span>

<span data-ttu-id="1bf84-117">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1bf84-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1bf84-118">Dodatkowe przykłady programu Azure Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1bf84-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
