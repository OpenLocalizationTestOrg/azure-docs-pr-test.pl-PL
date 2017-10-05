---
title: "Jak odinstalować narzędzia zadania elastycznej bazy danych"
description: "Jak odinstalować narzędzia zadania elastycznej bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="06d96-103">Odinstaluj składniki zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="06d96-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="06d96-104">**Zadania elastyczne bazy danych** składniki można odinstalować za pomocą portalu lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06d96-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="06d96-105">Odinstaluj składniki zadania elastycznej bazy danych przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="06d96-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="06d96-106">Otwórz [portal Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="06d96-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="06d96-107">Przejdź do subskrypcji, która zawiera **zadania elastycznej bazy danych** składniki, to znaczy subskrypcji, w których elastycznej bazy danych zostały zainstalowane składniki zadania.</span><span class="sxs-lookup"><span data-stu-id="06d96-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="06d96-108">Kliknij przycisk **Przeglądaj** i kliknij przycisk **grup zasobów**.</span><span class="sxs-lookup"><span data-stu-id="06d96-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="06d96-109">Wybierz grupę zasobów o nazwie "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="06d96-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="06d96-110">Usuń grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="06d96-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="06d96-111">Odinstaluj składniki zadania elastycznej bazy danych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="06d96-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="06d96-112">Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź do podkatalogu narzędzia w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x: typ **narzędzia cd**.</span><span class="sxs-lookup"><span data-stu-id="06d96-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="06d96-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > Narzędzia dysku cd</span><span class="sxs-lookup"><span data-stu-id="06d96-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="06d96-114">Wykonanie.\UninstallElasticDatabaseJobs.ps1 skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06d96-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="06d96-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > C:.\UninstallElasticDatabaseJobs.ps1 PS odblokowanie pliku\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >. \ UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="06d96-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="06d96-116">Lub po prostu, uruchom następujący skrypt, przy założeniu, domyślne wartości, jeśli w instalacji składników:</span><span class="sxs-lookup"><span data-stu-id="06d96-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="06d96-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06d96-117">Next steps</span></span>
<span data-ttu-id="06d96-118">Aby ponownie zainstalować zadania elastycznej bazy danych, zobacz [instalowania usługi zadania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="06d96-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="06d96-119">Omówienie zadania elastycznej bazy danych, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06d96-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


